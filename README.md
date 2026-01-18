[kali.py](https://github.com/user-attachments/files/24699090/kali.py)
from flask import Flask, render_template, request, redirect
import os

app = Flask(__name__)

UPLOAD_FOLDER = 'static/videos'
app.config['UPLOAD_FOLDER'] = UPLOAD_FOLDER

@app.route('/', methods=['GET', 'POST'])
def index():
    if request.method == 'POST':
        video = request.files['video']
        if video:
            video.save(os.path.join(UPLOAD_FOLDER, video.filename))
            return redirect('/')
    videos = os.listdir(UPLOAD_FOLDER)
    return render_template('index.html', videos=videos)

if __name__ == '__main__':
    app.run(debug=True)
