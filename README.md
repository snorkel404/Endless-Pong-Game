# Endless-Pong-Game
#First Project. Enjoy and leave feedback to improve.

#simple pong game

import turtle

wn = turtle.Screen()
wn.title("Pong by Snorkel404")
wn.bgcolor("black")
wn.setup(width=800, height=600)
wn.tracer(0)

#score
score_for_player1 = 0
score_for_player2 = 0


#by default shpes are 20 yby 20 pixels

#paddle 1
paddle_1 = turtle.Turtle()
paddle_1.speed(0)
paddle_1.shape("square")
paddle_1.color("blue")
paddle_1.shapesize(stretch_wid=5, stretch_len=1)
paddle_1.penup()
paddle_1.goto(-350, 0)

#paddle2
paddle_2 = turtle.Turtle()
paddle_2.speed(0)
paddle_2.shape("square")
paddle_2.color("red")
paddle_2.shapesize(stretch_wid=5, stretch_len=1)
paddle_2.penup()
paddle_2.goto(350, 0)
#ball

ball = turtle.Turtle()
ball.speed(0)
ball.shape("circle")
ball.color("yellow")
ball.penup()
ball.goto(0, 0)

#pen
pen = turtle.Turtle()
pen.speed(0)
pen.color("White")
pen.penup()
pen.hideturtle()
pen.goto(0, 260)
pen.write("Player 1: 0 Player 2: 0", align="center", font=("Courier", 24, "normal"))


#move it to the right and up 2 pixels posit
ball.dx = 0.2
ball.dy = -0.2

#functions to move
#paddle_1 moving up and down
def paddle_1_up():
        y = paddle_1.ycor()
        y += 20
        paddle_1.sety(y)

def paddle_1_down():
        y = paddle_1.ycor()
        y -= 20
        paddle_1.sety(y)

#paddle_2 moving up and down
def paddle_2_up():
        y = paddle_2.ycor()
        y += 20
        paddle_2.sety(y)

def paddle_2_down():
        y = paddle_2.ycor()
        y -= 20
        paddle_2.sety(y)

#moving the ball
#havea x and y coor movemnet



#keyboard bind
wn.listen()
wn.onkeypress(paddle_1_up, "w")
wn.onkeypress(paddle_1_down, "s")
wn.onkeypress(paddle_2_up, "Up")
wn.onkeypress(paddle_2_down, "Down")

#main game loop

while True:
        wn.update()
        ball.setx(ball.xcor() + ball.dx)
        ball.sety(ball.ycor() + ball.dy)

        #border for the balls to bounce
        if ball.ycor() > 290:
                ball.sety(290)
                ball.dy *= -1

        if ball.ycor() < -290:
                ball.sety(-290)
                ball.dy *= -1


        if ball.xcor() > 390:
                ball.goto(0, 0)
                ball.dx *= -1
                score_for_player1 += 1
                pen.clear()
                pen.write("Player 1: {}  Player 2: {}".format(score_for_player1, score_for_player2), align="center", font=("Courier", 24, "normal"))

        if ball.xcor() < -390:
                ball.goto(0, 0)
                ball.dx *= -1
                score_for_player2 += 1
                pen.clear()
                pen.write("Player 1: {}  Player 2: {}".format(score_for_player1, score_for_player2), align="center", font=("Courier", 24, "normal"))

        #Paddles and ball Bounce
        if (ball.xcor() > 340 and ball.xcor() < 350) and (ball.ycor() < paddle_1.ycor() + 40 and ball.ycor() > paddle_2.ycor() -40):
                ball.setx(340)
                ball.dx *= -1

        if (ball.xcor() < -340 and ball.xcor() > -350) and (ball.ycor() < paddle_2.ycor() + 40 and ball.ycor() > paddle_1.ycor() -40):
                ball.setx(-340)
                ball.dx *= -1
