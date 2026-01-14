# Git Intro Project

───────┬──────────────────────────────────────────────────────────────────────────────────────────────
       │ File: factorial.py
───────┼──────────────────────────────────────────────────────────────────────────────────────────────
   1   │ #!/usr/bin/python3
   2   │
   3   │ import sys
   4   │
   5   │ def factorial(n):
   6   │     result = 1
   7   │     while n > 1:
   8   │         result *= n
   9   │         n -= 1
  10   │     return result
  11   │
  12   │ f = factorial(int(sys.argv[1]))
  13   │ print(f)
───────┴──────────────────────────────────────────────────────────────────────────────────────────────

────┬──────────────────────────────────────────────────────────────────────────────────────────────
       │ File: print_arguments.py
───────┼──────────────────────────────────────────────────────────────────────────────────────────────
   1   │ #!/usr/bin/python3
   2   │
   3   │ import sys
   4   │
   5   │ for arg in sys.argv[1:]:
   6   │     print(arg)
───────┴─────────────────────────

 File: change_background.html
───────┼──────────────────────────────────────────────────────────────────────────────────────────────
   1   │ <!DOCTYPE html>
   2   │ <html lang="en">
   3   │ <head>
   4   │     <meta charset="UTF-8">
   5   │     <title>Change Background Color</title>
   6   │
   7   │     <style>
   8   │         body {
   9   │             font-family: Arial, sans-serif;
  10   │             text-align: center;
  11   │             padding-top: 50px;
  12   │         }
  13   │         button {
  14   │             padding: 10px 20px;
  15   │             font-size: 16px;
  16   │             cursor: pointer;
  17   │         }
  18   │     </style>
  19   │ </head>
  20   │
  21   │ <body>
  22   │     <p>Click the button to change the background color</p>
  23   │
  24   │     <button id="colorButton">Change Color</button>
  25   │
  26   │     <script>
  27   │         document.getElementById("colorButton").addEventListener("click", function () {
  28   │             changeBackgroundColor();
  29   │         });
  30   │
  31   │         function changeBackgroundColor() {
  32   │             // Generate a random color
  33   │             var randomColor = "#" + Math.floor(Math.random() * 16777215).toString(16);
  34   │             // Change the background color of the body
  35   │             document.body.style.backgroundColor = randomColor;
  36   │         }
  37   │     </script>
  38   │ </body>
  39   │ </html>
───────┴───────────────────────────────────────────────────────
