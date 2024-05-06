---
title: "Music Player GUI with Python"
datePublished: Mon May 06 2024 07:08:34 GMT+0000 (Coordinated Universal Time)
cuid: clvumekbs000t0amf0nxbdz3c
slug: music-player-gui-with-python
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1714978585133/f2e7c4d9-38e7-41c9-832a-22e919748139.webp
tags: music, python, beginner

---

A Music Player lets you manage and listen to all your music files quickly and easily. In this article, I will take you through how to create a Music Player GUI with Python.

### How To Create a Music Player GUI with Python

The first step is to choose a Python GUI framework, here i will use two main GUI libraries for creating a Music player with Python:

1. Pygame
    
2. Tkinter
    

Pygame is a Python library used to create video games. To create a music player with Python, we will be using the Pygame sound component.

Tkinter is a library for creating GUI applications. Here we don’t need to use much functions of it we just need to use the askdirectory() method of Tkinter and other methods that you will see in the code section below.

Then we will create functions such as play, stop, pause and resume in order to control the music player. To create these commands, we’ll build some functions and we’ll use Tkinter to create the button in the interface.

We are now going to implement all of the steps above in the section below to create a music player with Python.

#### Music Player GUI with Python:

```python
import pygame
import tkinter as tkr
from tkinter.filedialog import askdirectory
import os

music_player = tkr.Tk()
music_player.title("My Music Player")
music_player.geometry("450x350")
directory = askdirectory()
os.chdir(directory)
song_list = os.listdir()

play_list = tkr.Listbox(music_player, font="Helvetica 12 bold", bg='yellow', selectmode=tkr.SINGLE)
for item in song_list:
    pos = 0
    play_list.insert(pos, item)
    pos += 1
pygame.init()
pygame.mixer.init()

def play():
    pygame.mixer.music.load(play_list.get(tkr.ACTIVE))
    var.set(play_list.get(tkr.ACTIVE))
    pygame.mixer.music.play()
def stop():
    pygame.mixer.music.stop()
def pause():
    pygame.mixer.music.pause()
def unpause():
    pygame.mixer.music.unpause()
Button1 = tkr.Button(music_player, width=5, height=3, font="Helvetica 12 bold", text="PLAY", command=play, bg="blue", fg="white")
Button2 = tkr.Button(music_player, width=5, height=3, font="Helvetica 12 bold", text="STOP", command=stop, bg="red", fg="white")
Button3 = tkr.Button(music_player, width=5, height=3, font="Helvetica 12 bold", text="PAUSE", command=pause, bg="purple", fg="white")
Button4 = tkr.Button(music_player, width=5, height=3, font="Helvetica 12 bold", text="UNPAUSE", command=unpause, bg="orange", fg="white")

var = tkr.StringVar() 
song_title = tkr.Label(music_player, font="Helvetica 12 bold", textvariable=var)

song_title.pack()
Button1.pack(fill="x")
Button2.pack(fill="x")
Button3.pack(fill="x")
Button4.pack(fill="x")
play_list.pack(fill="both", expand="yes")
music_player.mainloop()
```

![](https://cdn-images-1.medium.com/max/800/1*GtDfSb2OusbVMkMZY9f4iA.png align="left")

Now you have your own music player and you can listen to songs using this app. Also, I think that creating such apps like a music player or other apps that you can use in your daily life can really help you get to know new Python frameworks and at the same time you will learn more about programming.

This is one of the best ways to improve your programming skills in building something or automating a process that gives you more confidence with programming skills and it is very helpful in boosting your portfolio.

I hope you liked this article on how to create a music player with Python. Feel free to ask your valuable questions in the comment section below. Thank You.