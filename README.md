# Gachon University TEAM 1

![](https://gaussian37.github.io/assets/img/vision/opencv/opencv.png)

---
## Refernece
>[Face Recognition](https://github.com/ageitgey/face_recognition)
[Dlib](http://dlib.net/)
[OpenCV2](https://opencv.org/ )
[Discord.py]( https://github.com/Rapptz/discord.py)
[Numpy](https://numpy.org/)

|Author & Collaborator|
|:--:|
|김충영|
|김준혁|
|김진성|
|김태우|
![Gachon][logo]

[logo]: /README_image/gachon.jpg?raw=true "Gachon."


## Purpose
- Alert-To-Discord can distinguishes unknowns and registered people for security.

- This project can be used in some private spaces such as workplace







---

## Feature
### (1) It recognizes faces through webcams.
```
    # show the frame
    cv2.imshow("Frame", frame)
    key = cv2.waitKey(1) & 0xFF
    if count==1: #if face is found, save as "cache.jpg"
        cv2.imwrite('./cache.jpg',frame)
        break
```
### (2) Check if the faces match to the pictures in "Knows" directory.
```
    # See if the face is a match for the known face(s)
    distances = face_recognition.face_distance(self.known_face_encodings, face_encoding)
    min_value = min(distances)

    # tolerance: How much distance between faces to consider it a match. Lower is more strict.
    # 0.6 is typical best performance.
    name = "Unknown"
    if min_value < 0.6:
        index = np.argmin(distances)
        name = self.known_face_names[index]
```
### (3) Send alert via discode bot
```
    if int(now - prev) > 10:
        if os.path.exists('./cache.jpg'):
            os.remove('./cache.jpg')

        cv2.imwrite('./cache.jpg', frame)
        with open('./cache.jpg', 'rb') as f:
            pic = discord.File(f)
            await ctx.send(file=pic)
            await ctx.send('Safety Alert!')
        prev = now
        os.remove('./cache.jpg')
```

### (4) Example of using this program.

![Example][ex]

[ex]: /README_image/taewoo2.png?raw=true "Example."




---
## NOTE
- You must create **Token_discord.py** and put the token value of the discode bot in the token_dis value. For security reasons, **Never expose a bot's token** to the public Internet.

- Although you did not import dlibs from your code, the face_recognition library is a library that uses the features of dlibs. **Therefore, you must have related libraries installed**, such as dlib and Cmake.

- When creating a Discord bot, **PRESENCE INTENT, SERVER MEMBERS INTENT, and MESSAGE CONTENT INTENT** must be enabled. Additional permission assignments can cause security issues.
---
## Known issues ![warning][warning]
- When the Face detect alert function is running, the record api turns off the gateway at certain times. I think it's to prevent wasting resources when there's no input. However, there seems to be no problem, seeing that the message is sent normally when it occurs.

- If *Face recognition* is not properly performed, an error may occur.

- The stop monitoring function has not yet been implemented because it has an infinite loop in it when entering the start command. Knowledge of asynchronous programming seems to be needed.
--- 
## How To Use 
- Create an application, bot, from the Discord Developer Portal at **(https://discord.com/developers/applications)**. Allow certain permissions, such as precautions, and then receive Token.

- Create **token_discord.py** in the project's top-level directory, create the **token_dis variable**, and enter the issued token.

- Put a picture of a known person's face inside the Knows folder. **Only Jpg files** are supported.

- Verify that the webcam is connected, and run record_bot_sender.py. When the Done. message appears in the Console, verify that the bot is online in the discode.
- **!start** command to start webcam monitoring.

[warning]: /README_image/warning_sign.jpg?raw=true "warning."





