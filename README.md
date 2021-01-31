# Ping-Pong
In this report we will see the different code lines of a python program, made by the visual studio code platform using a 32 bits python interpreter. This program will allow us to end up with a game called “AMINE Ping Pong Game In Python” 
#######################################################################
# Create a Ping Pong Application using juste one library called Turtle
########################################################################

#imported turtle module
import turtle

wn = turtle.Screen() #initializes screen
wn.title("AMINE Ping Pong Game In Python") #set the title of the window
wn.bgcolor("green") #set the background color of the window 
wn.setup(width=800, height=600) #set the width and the height of the window
wn.tracer(0) #stops the window from updating automatically


# madrab1 of the first player
madrab1 = turtle.Turtle() #initializes turtle object(shape) 
madrab1.speed(0) #set the speed of the animation
madrab1.shape("square") #set the shape of the object 
madrab1.color("red") #set the color of the shape
madrab1.shapesize(stretch_wid=5, stretch_len=1) #stretches the shape to meet the size
madrab1.penup() #stops the object from drawing lines 
madrab1.goto(-350, 0) #set the position of the object 

# madrab2 of the second player
madrab2 = turtle.Turtle()
madrab2.speed(0)
madrab2.shape("square")
madrab2.color("yellow")
madrab2.shapesize(stretch_wid=5, stretch_len=1)
madrab2.penup()
madrab2.goto(350, 0)

# ball
ball = turtle.Turtle()
ball.speed(0)
ball.shape("square")
ball.color("white")
ball.penup()
ball.goto(0, 0)
ball.dx = 0.4
ball.dy = 0.4

# score 
score1 = 0
score2 = 0
score = turtle.Turtle()
score.speed(0)
score.color("white")
score.penup()
score.hideturtle()
score.goto(0, 260)
score.write("Player I: 0   Player II: 0", align="center", font=("arial", 24, "normal"))


#functions
def madrab1_up():
    y = madrab1.ycor() #get the y coordinate of the madrab1
    y += 20 #set the y to increase with 20
    madrab1.sety(y) #set the y of the madrab1 tothe new y coordinate

def madrab1_down():
    y = madrab1.ycor()
    y -= 20 #set the y to decrease with 20
    madrab1.sety(y)

def madrab2_up():
    y = madrab2.ycor()
    y += 20
    madrab2.sety(y)

def madrab2_down():
    y = madrab2.ycor()
    y -= 20
    madrab2.sety(y)

#keyboard bindings
wn.listen() #tell the window to expect keyboard input
wn.onkeypress(madrab1_up, "g") #when pressing g the function madrab1_up is invoked
wn.onkeypress(madrab1_down, "n") 
wn.onkeypress(madrab2_up, "Up")
wn.onkeypress(madrab2_down, "Down")

# main game loop
while True:
    wn.update() #updates the screen everytime the loop run

    #move the ball
    ball.setx(ball.xcor() + ball.dx) #ball starts at 0 and everytime loops run -->+0.4 x axis
    ball.sety(ball.ycor() + ball.dy) #ball starts at 0 and everytime loops run -->+0.4 y axis

    #border check , top border +300px, bottom border -300px, ball is 20px
    if ball.ycor() >290: #if ball is at top border
        ball.sety(290) #set y cordinate +290
        ball.dy *= -1 #reverse direction, making +0.4-->-0.4

    if ball.ycor() <-290: #if ball is at bottom border
        ball.sety(-290)
        ball.dy *= -1
    
    if ball.xcor() >390: #if ball is at right border
        ball.goto(0, 0) #return ball to center
        ball.dx *= -1 #reverses the x direction
        score1 += 1
        score.clear()
        score.write("Player I: {}  Player II: {}".format(score1, score2), align="center", font=("arial", 24, "normal"))

    if ball.xcor() <-390: #if ball is at left border
        ball.goto(0, 0)
        ball.dx *= -1 
        score2 += 1
        score.clear()
        score.write("Player I: {}  Player II: {}".format(score1, score2), align="center", font=("arial", 24, "normal"))

    
    #collision between madrab and ball
    if (ball.xcor() > 340 and ball.xcor() < 350) and (ball.ycor() < madrab2.ycor() + 40 and ball.ycor() > madrab2.ycor() - 40):
        ball.setx(340)
        ball.dx *= -1

    if (ball.xcor() < -340 and ball.xcor() > -350) and (ball.ycor() < madrab1.ycor() + 40 and ball.ycor() > madrab1.ycor() - 40):
        ball.setx(-340)
        ball.dx *= -1
