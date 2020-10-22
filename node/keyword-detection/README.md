# Flexible Electric Owl

### **Region:**
Americas

### **Team Members**:
John Lafer  
Lilllan Wakefield  
Mark Shavers

---

### Project Overview
This project is to improve the experience of call center agents by using transcription analysis of real time conversations to be able to detect when an agent could use assistance.  Once this signal has been detected a visual queue will be displayed to a designated resource and they will be able to proactively contact the agent and offer assistance.

## App sever setup

### Create a new IBM Cloud Resource

https://cloud.ibm.com/catalog/services/speech-to-text

On the **Credentials** card choose the **Download** link. Save the file ibm-credentials.env in the same folder as this file.

### Installation

**Requires Node >= v12**

Run `npm install`

#### Running the server

Start with `npm start happy angry`

## Setup

Replace `<Your-Agent-Path>` on line 65 in `index.js` with your Electric Imp agent path.


You can setup your environment to run the demo by using the CLI (BETA) or the Console.

### Configure using the CLI

1. Find available phone number
`twilio api:core:available-phone-numbers:local:list --country-code="US" --voice-enabled --properties="phoneNumber"`

2. Purchase the phone number (where `+123456789` is a number you found)
`twilio api:core:incoming-phone-numbers:create --phone-number="+123456789"`

3. Start ngrok
`ngrok http 8080`

4. Wire up an incoming call handler to your number using a **TwiML Bin**
```
<?xml version="1.0" encoding="UTF-8"?>
<Response>
  <Start>
    <Stream url="wss://<Your ngrok host name here>.ngrok.io/media" />
  </Start>
  <Pause length="40" />
</Response>
```

5. Call your number `+123456789` from a phone.

6. Speak the keywords and see them get detected in realtime
