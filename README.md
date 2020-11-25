# Pong-Game-using-Turtle

from turtle import *
import turtle

wn = turtle.Screen()
wn.title("Pong Game")
wn.bgcolor("Black")
wn.setup(width = 800, height = 600)
wn.tracer(0)

#Paddle A
paddleA = turtle.Turtle()
paddleA.speed(0)
paddleA.shape("square")
paddleA.color("white")
paddleA.penup()
paddleA.shapesize(stretch_len= 1, stretch_wid= 5)
paddleA.goto(-720, 0)

#paddleB
paddleB = turtle.Turtle()
paddleB.speed(0)
paddleB.shape("square")
paddleB.color("white")
paddleB.penup()
paddleB.shapesize(stretch_len= 1, stretch_wid= 5)
paddleB.goto(720, 0)


#Ball
ball = turtle.Turtle() # small T=for module name and capital T=for the class name
ball.speed(0)
ball.shape("circle")
ball.color("white")
ball.penup()
ball.goto(0, 0)
ball.dx = 0.3 #speed of the ball through x-coordinate...here - sign represents movement of ball in down direction
ball.dy = 0.3
score_a = 0
score_b = 0

#Pen--Scores
pen = turtle.Turtle()
pen.speed(0)
pen.speed(0)
pen.color("white")
pen.penup()
pen.hideturtle()
pen.goto(0, 330)
pen.write("PlayerA:0  PlayerB:0" ,align = "center", font = ("courier", 24,"normal"))


def paddleA_up():
    y = paddleA.ycor()
    y += 30
    paddleA.sety(y)

def paddleB_up():
    y = paddleB.ycor()
    y += 30
    paddleB.sety(y)

def paddleA_down():
    y = paddleA.ycor()
    y -= 30
    paddleA.sety(y)

def paddleB_down():
    y = paddleB.ycor()
    y -= 30
    paddleB.sety(y)

#Keyboard Bindings
wn.listen()
wn.onkeypress(paddleA_up,"w")

wn.listen()
wn.onkeypress(paddleB_up,"i")

wn.listen()
wn.onkeypress(paddleA_down,"z")

wn.listen()
wn.onkeypress(paddleB_down,"m")

while True:
    wn.update()

    ball.setx(ball.xcor() + ball.dx)
    ball.sety(ball.ycor() + ball.dy)

    if ball.ycor() > 390:
        ball.sety(390)
        ball.dy *= -1 # speed of ball is reversed in opposite direction if ball hits the borders
    if ball.ycor() < -390:
        ball.sety(-390)
        ball.dy *= -1


    if ball.xcor() > 790:
      ball.goto(0, 0)
      ball.dx *= -1
      score_a += 1
      pen.clear()
      pen.write("PlayerA:{}  PlayerB:{}".format(score_a,score_b), align="center", font=("courier", 24, "normal"))

    if ball.xcor() < -790:
      ball.goto(0, 0)
      ball.dx *= -1
      score_b += 1
      pen.clear()
      pen.write("PlayerA:{}  PlayerB:{}".format(score_a,score_b), align="center", font=("courier", 24, "normal"))

    #Paddle and ball collisions
    if (ball.xcor() > 695 and ball.xcor() < 710) and (ball.ycor() < paddleB.ycor() + 40 and ball.ycor() > paddleB.ycor() - 40):
      ball.setx(695)
      ball.dx *= -1
      
    if (ball.xcor() < -695 and ball.xcor() > -710) and (ball.ycor() < paddleA.ycor() + 40 and ball.ycor() > paddleA.ycor() - 40):
      ball.setx(-695)
      ball.dx *= -1
      
