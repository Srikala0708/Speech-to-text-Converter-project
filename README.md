# Speech-to-text-Converter-project
Code of Speech to text Coverter
<!DOCTYPE html
<html>
<head>
    <!-- Meta tags and title... -->
    <style>
        /* CSS styles... */
        
        body{
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            font-family: Arial, Helvetica, sans-serif;
            background-color: #f5f5f5;
        }

        .container{
            background-color: white;
            box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
            border-radius: 10px;
            padding: 20px;
            text-align: center;
        }

        .title{
            color: black;
            margin-bottom: 20px;
        }

        .buttons {
            display: flex;
            justify-content: center;
            gap: 10px;
        }

        button{
            background-color: #4CAF50;
            border: none;
            color: white;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 14px;
        } 

        button:hover{
            background-color: #45a049;
            transform: scale(1.05);
        }

        button:disabled{
            background-color: #ccc;
            cursor: not-allowed;
        }

        .outputText{
            margin-top: 20px;
            min-height: 100px;
            background-color: #f5f5f5;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 16px;
        }
    
    

    </style>
</head>
<body>
    <div class="container">
        <h1 class="title"> Speech to Text</h1>
        <div class="buttons">
            <button id="startButton"> Start Listening </button>
            <button id="stopButton" disabled> Stop Listening </button>
        </div>
        <div id="output" class="outputText"></div>
    </div>

    <script>
        // JavaScript code...
        const startButton = document.getElementById('startButton')
        const stopButton = document.getElementById('stopButton');
        const outputDiv = document.getElementById('output');
        const recognition = new webkitSpeechRecognition() || new SpeechRecognition();

        recognition.interimResults = true;
        recognition.continuous = true;

        startButton.addEventListener('click', () => {
            recognition.start();
            startButton.disabled = true;
            stopButton.disabled = false;
            startButton.textContent = 'Recording...';
        });

        stopButton.addEventListener('click', () => {
            recognition.stop();
            stopButton.disabled = true;
            startButton.disabled = false; 
            startButton.textContent = 'Start Recording';
        });

        recognition.onresult = event => {
            const result = event.results[event.results.length - 1][0].transcript;
            outputDiv.textContent = result;
        };
        
        recognition.onend = () => {
            stopButton.disabled = true;
            startButton.disabled = false;
            startButton.textContent = 'Start Recording';
        };
        
        recognition.onerror = event => {
            console.error('Speech recognition error:', event.error);
        };
        
        recognition.onnomatch = () => {
            console.log('No speech was recognized.');
        };
    </script>
</body>
</html>
