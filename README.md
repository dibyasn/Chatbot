# Chatbot

---


<p align="center">
    <img src="https://github.com/dibyasn/Chatbot/assets/42934757/89058190-5d73-49ba-9258-5e6ee78dd20a" alt="Chatbot" style: width="400px;">
</p>


Welcome to the Kids Chat Bot project! This interactive chatbot is designed to be fun and engaging for kids, using the Gemini API to provide answers to their questions. This README will guide you through the steps to set up, customize, and run the project.

## Table of Contents

- [Chatbot](#chatbot)
  - [Table of Contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Features](#features)
  - [Prerequisites](#prerequisites)
  - [Setup](#setup)
  - [Usage](#usage)
  - [Customization](#customization)
  - [Troubleshooting](#troubleshooting)
  - [Acknowledgements](#acknowledgements)
  - [Code](#code)
  - [Contributing](#contributing)

## Introduction

The Kids Chat Bot is a web-based application that uses the Gemini API to generate responses to user questions. It's built with HTML, CSS (Bootstrap), and JavaScript, ensuring a responsive and interactive experience suitable for kids.

## Features

- Interactive chat interface
- Responsive design for various devices
- Clear chat history button
- Download chat history as a text file
- API key submission for secure access to Gemini API

## Prerequisites

To run this project, you need:

- A web browser (Google Chrome, Firefox, Safari, etc.)
- An API key from [Gemini AI Studio](https://aistudio.google.com/app/apikey)

## Setup

Follow these steps to set up the Kids Chat Bot:

1. **Get Your API Key**
   - Visit [Gemini AI Studio](https://aistudio.google.com/app/apikey)
   - Sign in or create an account
   - Generate your API key

2. **Download or Clone the Project**
   - Download the project ZIP file from the repository or clone it using Git:
     ```sh
     git clone https://github.com/dibyasn/Chatbot.git
     ```

3. **Open the Project**
   - Extract the ZIP file (if downloaded)
   - Open the `gemini.html` file in your web browser

## Usage

1. **Enter Your API Key**
   - On the top of the page, enter your Gemini API key in the provided input box
   - Click the "Submit API Key" button

2. **Ask Questions**
   - Type your question in the input box at the bottom
   - Press "Enter" or click the "Send" button to submit your question

3. **Interact with the Bot**
   - The bot will respond to your questions using the Gemini API
   - The conversation will appear in the chat box

4. **Clear and Download Chat**
   - Use the "Clear" button to clear the chat history
   - Use the "Download Chat" button to download the chat history as a text file

## Customization

You can customize the Kids Chat Bot by modifying the HTML, CSS, and JavaScript. Here are some ideas:

- **Change the Theme**: Modify the CSS to change the colors, fonts, and styles
- **Add New Features**: Enhance the JavaScript to add new functionalities
- **Personalize Responses**: Customize the bot's responses for a more personalized experience

## Troubleshooting

If you encounter issues, consider the following:

- **API Key Issues**: Ensure your API key is valid and correctly entered
- **Network Issues**: Check your internet connection
- **Browser Issues**: Ensure you are using an up-to-date web browser

## Acknowledgements

This project was inspired by the need for an interactive, educational tool for kids. Special thanks to the creators of the Gemini API for providing a powerful tool for generating AI responses.

---

## Code

Below is the complete code for the Kids Chat Bot:

```html
<!DOCTYPE html>
<html>
<head>
  <title>Kids Chat Bot</title>
  <link href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" rel="stylesheet">
  <style>
    body {
      font-family: 'Comic Sans MS', 'Comic Sans', cursive;
      background-color: #f0f8ff;
    }
    .chat-container {
      max-width: 600px;
      margin: 50px auto;
      padding: 20px;
      border-radius: 10px;
      background-color: #fff;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    .chat-box {
      height: 400px;
      overflow-y: scroll;
      border: 1px solid #ccc;
      border-radius: 10px;
      padding: 10px;
      background-color: #e6f7ff;
    }
    .chat-box div {
      margin: 10px 0;
    }
    .question {
      font-weight: bold;
      color: #ff6347;
    }
    .answer {
      margin-left: 20px;
      color: #4682b4;
    }
    .input-box {
      margin-top: 20px;
    }
    .input-box input[type="text"] {
      width: calc(100% - 90px);
      padding: 10px;
      border-radius: 20px;
      border: 2px solid #87ceeb;
    }
    .submit-btn {
      padding: 10px 20px;
      border-radius: 20px;
      border: none;
      background-color: #87ceeb;
      color: #fff;
      cursor: pointer;
      transition: background-color 0.3s, transform 0.3s;
    }
    .submit-btn:hover {
      background-color: #4682b4;
      transform: scale(1.1);
    }
    .input-box input[type="submit"] {
      padding: 10px 20px;
      border-radius: 20px;
      border: none;
      background-color: #87ceeb;
      color: #fff;
      cursor: pointer;
      transition: background-color 0.3s;
    }
    .input-box input[type="submit"]:hover {
      background-color: #4682b4;
    }
    .button-box {
      margin-top: 10px;
    }
    .button-box button {
      padding: 10px 20px;
      border-radius: 20px;
      border: none;
      background-color: #87ceeb;
      color: #fff;
      cursor: pointer;
      transition: background-color 0.3s;
      margin: 5px;
    }
    .button-box button:hover {
      background-color: #4682b4;
    }
    .api-key-box {
      margin-bottom: 20px;
    }
  </style>
</head>
<body>
  <div class="container chat-container">
    <h1 class="text-center mb-4">Kids Chat Bot</h1>
    <div class="api-key-box text-center">
      <input type="text" id="apiKey" class="form-control d-inline" placeholder="Enter your Gemini API key...">
      <button class="btn d-inline submit-btn" onclick="submitApiKey()">Submit API Key</button>
    </div>
    <div class="chat-box" id="chat-box"></div>
    <div class="input-box text-center">
      <input type="text" id="question" class="form-control d-inline" placeholder="Type your question here..." onkeypress="handleKeyPress(event)">
      <input type="submit" class="btn d-inline" value="Send" onclick="sendQuestion()">
    </div>
    <div class="button-box text-center">
      <button onclick="clearChat()">Clear</button>
      <button onclick="downloadChat()">Download Chat</button>
    </div>
  </div>

  <script>
    let geminiToken = "";

    function submitApiKey() {
      geminiToken = document.getElementById('apiKey').value.trim();
      if (!geminiToken) {
        alert('Please enter a valid API key!');
        return;
      }
      document.getElementById('apiKey').value = '';  // Clear the input field after submission
      document.getElementById('apiKey').placeholder = '******';  // Change placeholder after submission
      document.getElementById('apiKey').disabled = true;  // Disable the input field after submission
      alert('API Key submitted successfully!');
    }

    async function sendQuestion() {
      const question = document.getElementById('question').value;
      if (!question) return;

      const chatBox = document.getElementById('chat-box');
      const userQuestionDiv = document.createElement('div');
      userQuestionDiv.className = 'question';
      userQuestionDiv.textContent = 'You: ' + question;
      chatBox.appendChild(userQuestionDiv);

      const payload = {
        contents: [{ parts: [{ text: question }] }],
        generationConfig: { maxOutputTokens: 10000 }
      };

      const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${geminiToken}`, {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(payload)
      });

      if (response.ok) {
        const result = await response.json();
        const answer = result.candidates[0].content.parts[0].text;

        const botAnswerDiv = document.createElement('div');
        botAnswerDiv.className = 'answer';
        botAnswerDiv.textContent = 'Bot: ' + answer;
        chatBox.appendChild(botAnswerDiv);

        chatBox.scrollTop = chatBox.scrollHeight;  // Scroll to the bottom
        document.getElementById('question').value

 = '';  // Clear the input field
      } else {
        const errorDiv = document.createElement('div');
        errorDiv.className = 'answer text-danger';
        errorDiv.textContent = 'Error: Unable to get a response from the API';
        chatBox.appendChild(errorDiv);
      }
    }

    function handleKeyPress(event) {
      if (event.key === 'Enter') {
        sendQuestion();
      }
    }

    function clearChat() {
      const chatBox = document.getElementById('chat-box');
      chatBox.innerHTML = '';
    }

    function downloadChat() {
      const chatBox = document.getElementById('chat-box');
      const chatText = chatBox.innerText;
      const blob = new Blob([chatText], { type: 'text/plain' });
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.href = url;
      a.download = 'chat.txt';
      a.click();
      URL.revokeObjectURL(url);
    }
  </script>
</body>
</html>
```

## Contributing

We welcome contributions! Feel free to open issues or submit pull requests for improvements and new features.

<p align="center">
    <img src="https://64.media.tumblr.com/tumblr_lp0f2fIhnF1qa2ip8o1_1280.gif" alt="Thank You">
</p>

---

Feel free to contribute, report issues, or suggest enhancements. Happy coding! 🚀

<p align="center">
    <a href="https://github.com/dibyasn/Analog_clock"><img src="https://img.icons8.com/color/48/000000/github.png" alt="Contribute Icon"></a>
</p>
