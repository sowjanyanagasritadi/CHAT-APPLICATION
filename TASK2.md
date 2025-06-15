from flask import Flask, render_template
from flask_socketio import SocketIO, send

app = Flask(_name_)
app.config['SECRET_KEY'] = 'your_secret_key'
socketio = SocketIO(app, cors_allowed_origins="*")

@app.route('/')
def index():
    return render_template('chat.html')

@socketio.on('message')
def handleMessage(msg):
    print('Message: ' + msg)
    send(msg, broadcast=True)

if _name_ == '_main_':
    socketio.run(app, debug=True)
