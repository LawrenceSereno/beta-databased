# How to Run a Local Web Server

## The Problem

Opening HTML files directly (using `file://` protocol) causes CORS errors with ES6 modules. You need to run a local web server.

## Solution: Use a Local Web Server

### Option 1: Python (Easiest - Works on Windows/Mac/Linux)

1. **Open Terminal/Command Prompt** in your project folder:
   ```bash
   cd C:\Users\Administrator\Downloads\website-connect
   ```

2. **Run Python server:**
   
   **Python 3:**
   ```bash
   python -m http.server 8000
   ```
   
   **Python 2:**
   ```bash
   python -m SimpleHTTPServer 8000
   ```

3. **Open browser** and go to:
   ```
   http://localhost:8000/firebase-init.html
   ```

4. **To stop the server:** Press `Ctrl+C` in the terminal

---

### Option 2: Node.js (If you have Node.js installed)

1. **Install http-server globally:**
   ```bash
   npm install -g http-server
   ```

2. **Navigate to your project folder:**
   ```bash
   cd C:\Users\Administrator\Downloads\website-connect
   ```

3. **Start the server:**
   ```bash
   http-server -p 8000
   ```

4. **Open browser** and go to:
   ```
   http://localhost:8000/firebase-init.html
   ```

---

### Option 3: VS Code Live Server (Recommended for Development)

1. **Install VS Code** (if not already installed)

2. **Install Live Server extension:**
   - Open VS Code
   - Go to Extensions (Ctrl+Shift+X)
   - Search for "Live Server"
   - Install by Ritwick Dey

3. **Open your project folder** in VS Code

4. **Right-click on `firebase-init.html`**
   - Select "Open with Live Server"
   - Browser will open automatically

---

### Option 4: PHP (If you have PHP installed)

1. **Navigate to your project folder:**
   ```bash
   cd C:\Users\Administrator\Downloads\website-connect
   ```

2. **Start PHP server:**
   ```bash
   php -S localhost:8000
   ```

3. **Open browser** and go to:
   ```
   http://localhost:8000/firebase-init.html
   ```

---

## Quick Test

After starting a server, you should be able to:
1. Open `http://localhost:8000/firebase-init.html`
2. See "Firebase Database connected" in the log
3. Click "Initialize Firebase Data" button
4. See data being initialized

## Troubleshooting

### "Firebase Database not initialized"
- Make sure you're using `http://localhost:8000` not `file://`
- Check browser console for errors
- Make sure Firebase config is correct

### "Port already in use"
- Use a different port: `python -m http.server 8080`
- Or stop the other server using that port

### "Python not found"
- Install Python from [python.org](https://www.python.org/)
- Or use one of the other options above

---

## Recommended: Use Python

**Python is the easiest option** - it's usually already installed on most systems:

```bash
# Navigate to project folder
cd C:\Users\Administrator\Downloads\website-connect

# Start server
python -m http.server 8000

# Open browser to:
# http://localhost:8000/firebase-init.html
```

That's it! 🎉

