Video: https://www.youtube.com/watch?v=D4fE_v8f9-U

# ___QUAD PONG___
#Domenic Malinsky 2021
#Credit For Christian Thompson @TokyoEdTech for the basic starter guide on 2 player pong.

"""
Controls: [RED: W S ] [BLUE: UP DOWN] [PURPLE: NUM 1 NUM 2 ] [GREEN: G H ] ~~~ make sure caps lock is off ~~~
Rules: 
        1. This is kind of like a unfair game of pong, you play for yourself but must watch for others because you only score on the opposite of your position
        so it might be worth to think when you want to let the ball pass and when you wanna bounce it back. 
        2. There is no score limit you can go for as long as you want do not stress over who wins it will take the focus away from the game.
"""
'''
Overall creating the basic two player pong was simple because of all the helpful guides out there, but the problem that I came across when making my quad pong
was detecting the other two paddles, after some messing with the numbers and directional parts I managed to figure out the problem and made it work right after 
fixing it.
'''


#---_____CODE BELOW_____---
import turtle
import os
import wave
import pygame
import sys
from tkinter import *

#song = wave.open("C:\Users\Domenic Malinsky\Desktop\Code\Python\GAME\ancients.mp3", "r")
#p = vlc.MediaPlayer("C:\Users\Domenic Malinsky\Desktop\Code\Python\GAME\ancients.mp3")
#p.play()
#os.system("afplay ancients.mp3")-mac(feels bad man)

title = Tk()
title.title("Quad Pong")
label_1 = Label(title, text = "Welcome To Quad Pong")
label_2 = Label(title, text = "RULES")
label_3 = Label(title, text = "1. This is kind of like an unfair game of pong, you play for yourself but must watch for others because you only score on the opposite of your position")
label_4 = Label(title, text = "so it might be worth to think when you want to let the ball pass and when you wanna bounce it back.")
label_5 = Label(title, text = "2. There is no score limit you can go for as long as you want do not stress over who wins it will take the focus away from the game.")
label_6 = Label(title, text = "Also the game has already started so congrates on the person who picked the purple paddle.")
label_7 = Label(title, text = "[RED: W S ] [BLUE: UP DOWN] [PURPLE: NUM 1 NUM 2 ] [GREEN: G H ] ~~~ make sure caps lock is off ~~~")
label_1.pack()
label_2.pack()
label_3.pack()
label_4.pack()
label_5.pack()
label_6.pack()
label_7.pack()

wn = turtle.Screen()
wn.title("Quad Pong")
wn.bgcolor("grey")
wn.setup(width=1000, height=800)
wn.tracer(0)

#Border
bd = turtle.Turtle()
bd.penup()
bd.goto(-370,-270)
bd.pendown()
bd.pensize(5)
bd.fd(740)
bd.left(90)
bd.fd(540)
bd.left(90)
bd.fd(740)
bd.left(90)
bd.fd(540)
bd.hideturtle()

#Score
score_a = 0
score_b = 0
score_c = 0
score_d = 0

#Paddle A
paddle_a = turtle.Turtle()
paddle_a.speed(3)
paddle_a.shape("square")
paddle_a.color("red")
paddle_a.shapesize(stretch_wid=4,stretch_len=1)
paddle_a.penup()
paddle_a.goto(-350, 0)

#Paddle B
paddle_b = turtle.Turtle()
paddle_b.speed(3)
paddle_b.shape("square")
paddle_b.color("blue")
paddle_b.shapesize(stretch_wid=4,stretch_len=1)
paddle_b.penup()
paddle_b.goto(350, 0)

#Paddle C
paddle_c = turtle.Turtle()
paddle_c.speed(3)
paddle_c.shape("square")
paddle_c.color("green")
paddle_c.shapesize(stretch_wid=1,stretch_len=4)
paddle_c.penup()
paddle_c.goto(0, 250)

#Paddle D
paddle_d = turtle.Turtle()
paddle_d.speed(3)
paddle_d.shape("square")
paddle_d.color("purple")
paddle_d.shapesize(stretch_wid=1,stretch_len=4)
paddle_d.penup()
paddle_d.goto(0, -250)

#Ball
ball = turtle.Turtle()
ball.speed(0)
ball.shape("circle")
ball.color("black")
ball.penup()
ball.goto(0, 0)
ball.dx = 0.3
ball.dy = 0.3

#Pen
pen = turtle.Turtle()
pen.speed(0)
pen.shape("square")
pen.color("white")
pen.penup()
pen.hideturtle()
pen.goto(0, 350)
pen.write("Player RED: 0  Player BLUE: 0  Player PURPLE: 0  Player GREEN: 0", align="center", font=("Courier", 19, "bold"))

# ---Moving Paddles--- 
# Numbers mean how many incraments the paddle moves for respective paddle direction.
#Paddle A
def paddle_a_up():
    y = paddle_a.ycor()
    y += 50
    paddle_a.sety(y)

def paddle_a_down():
    y = paddle_a.ycor()
    y -= 50
    paddle_a.sety(y)

#Paddle B
def paddle_b_up():
    y = paddle_b.ycor()
    y += 50 
    paddle_b.sety(y)

def paddle_b_down():
    y = paddle_b.ycor()
    y -= 50
    paddle_b.sety(y)

#Paddle C
def paddle_c_left():
    x = paddle_c.xcor()
    x += 50
    paddle_c.setx(x)

def paddle_c_right():
    x = paddle_c.xcor()
    x -= 50
    paddle_c.setx(x)

#Paddle D
def paddle_d_left():
    x = paddle_d.xcor()
    x += 50
    paddle_d.setx(x)

def paddle_d_right():
    x = paddle_d.xcor()
    x -= 50
    paddle_d.setx(x)

def start_key():
    start = start_key

#Keyboard Bindings
wn.listen()

wn.onkeypress(paddle_a_up, "w")
wn.onkeypress(paddle_a_down, "s")
wn.onkeypress(paddle_b_up, "Up")
wn.onkeypress(paddle_b_down, "Down")

wn.onkeypress(paddle_c_left, "h")
wn.onkeypress(paddle_c_right, "g")
wn.onkeypress(paddle_d_right, "1")
wn.onkeypress(paddle_d_left, "2")

# ___MAIN___
while True:
    wn.update()
    
    #Ball Location
    ball.setx(ball.xcor() + ball.dx)
    ball.sety(ball.ycor() + ball.dy)

    #Scoring 
    if ball.xcor() > 350:
        score_a += 1
        pen.clear()
        pen.write("Player RED: {}  Player BLUE: {} Player PURPLE: {} Player GREEN: {}".format(score_a, score_b, score_c, score_d), align="center", font=("Courier", 19, "bold"))
        ball.goto(0, 0)
        ball.dx *= -1

    elif ball.xcor() < -350:
        score_b += 1
        pen.clear()
        pen.write("Player RED: {}  Player BLUE: {} Player PURPLE: {} Player GREEN: {}".format(score_a, score_b, score_c, score_d), align="center", font=("Courier", 19, "bold"))
        ball.goto(0, 0)
        ball.dx *= -1
    
    elif ball.ycor() > 260:
        score_c += 1
        pen.clear()
        pen.write("Player RED: {}  Player BLUE: {} Player PURPLE: {} Player GREEN: {}".format(score_a, score_b, score_c, score_d), align="center", font=("Courier", 19, "bold"))
        ball.goto(0, 0)
        ball.dx *= -1
    
    elif ball.ycor() < -260:
        score_d += 1
        pen.clear()
        pen.write("Player RED: {}  Player BLUE: {} Player PURPLE: {} Player GREEN: {}".format(score_a, score_b, score_c, score_d), align="center", font=("Courier", 19, "bold"))
        ball.goto(0, 0)
        ball.dx *= -1
    

    #Paddle and Ball Collisions
    #RED PADDLE
    if ball.xcor() < -340 and ball.ycor() < paddle_a.ycor() + 50 and ball.ycor() > paddle_a.ycor() - 50:
        ball.dx *= -1 

    #BLUE PADDLE    
    elif ball.xcor() > 340 and ball.ycor() < paddle_b.ycor() + 50 and ball.ycor() > paddle_b.ycor() - 50:
        ball.dx *= -1

    #GREEN PADDLE
    elif ball.ycor() > 240 and ball.xcor() < paddle_c.xcor() + 50 and ball.xcor() > paddle_c.xcor() - 50:
        ball.dy *= -1 

    #PURPLE PADDLE
    elif ball.ycor() < -240 and ball.xcor() < paddle_d.xcor() + 50 and ball.xcor() > paddle_d.xcor() - 50: 
        ball.dy *= -1
    
   
    #score_a = 10 or score_b = 10 or score_c = 10 or score_d = 10 ------- (might use) piece to create a score limit
    #scoring works for all four players, but after adding the two extra paddles trouble figuring out the boundries for the ball to bounce off each paddle

    #____ISSUES____
    #note ----commenting out lines (164 - 174) and (191 - 203) and (215 - 221) allows for you to play the two player version---- (if four player did not work) [SOLVED]
    # scoring works for all four sides only issue is getting the green and purple paddles to work. [after a couple of attempts the problem was solved] [SOLVED]
