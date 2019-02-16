from graphics import *
from ast import literal_eval as make_tuple



# This function takes two python lists.  The first must be a 
# 2x2 array, and the second must be a 2x1 array (a 2 entry list), and it 
# returns the matrix product of the 2x2 matrix and the 2x1 vector
def matrix_mult(transfer, vector):
    new_vector = [0,0]
    new_vector[0]=transfer[0][0]*vector[0]+transfer[0][1]*vector[1]
    new_vector[1]=transfer[1][0]*vector[0]+transfer[1][1]*vector[1]

    return new_vector




# This function takes a transfer matrix and a graphics window and draws
# green lines on the graphics window in relation to the points in a file
# called "data.txt"  The points in data.txt must be entered as (x,y) followed
# by a newline.  A line will be drawn between each successive point in the
# "data.txt" file, dot-to-dot style unless a blank line (newline character) 
# is the only entry on a line of the file.  This is the signal to end the 
# previous line or "pick the pen off the paper" and begin the next line at 
# a new point.  Each point in "data.txt" will be multiplied by the values in
# the transfer matrix, and the resulting points and lines will be displayed on
# the screen.   To display the points of "data.txt" in their original form, use
# the identity matrix [1,0][[0,1]. 
def draw_picture(transfer_matrix, window):
    
    myfile = open('data.txt', 'r')
    line_list = []
    new_object = True

    for text_line in myfile:
        if text_line != "\n":
            if new_object:
                old_point = make_tuple(text_line)
                old_point = matrix_mult(transfer_matrix, old_point)
                new_object = False

            point = make_tuple(text_line)
            point = matrix_mult(transfer_matrix, point)

            line = Line(Point( (old_point[0]), (old_point[1]) ), 
                        Point( (point[0]), (point[1]) )  )
            line.setOutline(color_rgb(0,255,0))
            line.draw(window)
            line_list.append(line)
            old_point= point

        else:
            new_object = True
    
    return line_list


def main():

    transfer_matrix = [[1,2],[3,4]]

    keep_open= True

    #Open the Canvas window and set the size
    win_height = 700
    win_width = 700
    win = GraphWin("My Window", win_height, win_width)
    win.setBackground(color_rgb(0,0,0))
    win.setCoords(
        int( (win_width/2)*-1  ),
        int( (win_height/2)*-1 ),
        int( (win_width/2)     ),
        int( (win_height/2)    ))

    #Draw the x axis halfway up the window (y=0) and color it red
    x_axis=Line(
        Point( int( (win_width/2) *-1 ),  0),
        Point( int( (win_width/2)     ),  0)  
        )
    x_axis.setFill("red")
    x_axis.draw(win)



    #Draw the y axis halway across the window (x=0) and color it blue
    y_axis=Line(
        Point( 0,  int( (win_height/2) *-1) ),
        Point( 0,  int( (win_height/2) )    )  
        )
    y_axis.setFill("blue")
    y_axis.draw(win)


    #Draw the "quit" text near the bottom of the window
    exit_text=Text(
        Point(0,  int (win_height*-7/16 ) ),
        "Quit")
    exit_text.setTextColor("white")
    exit_text.setSize(32)
    exit_text.draw(win)




    #These lines place 4 text boxes near the upper left corner of the screen
    #These text boxes are the inputs for the transform matrix
    input00_box=Entry(
        Point( int( (win_width*3/8) ) ,  int ( ( win_height*7/16) ) ),
        5)
    input00_box.setText(  str(transfer_matrix[0][0]))
    input00_box.draw(win)

    input01_box=Entry(
        Point( int( (win_width*7/16) ) ,  int ( ( win_height*7/16) ) ),
        5)
    input01_box.setText(  str(transfer_matrix[0][1]))
    input01_box.draw(win)

    input10_box=Entry(
        Point( int( (win_width*3/8) ) ,  int ( ( win_height*3/8) ) ),
        5)
    input10_box.setText(  str(transfer_matrix[1][0]))
    input10_box.draw(win)

    input11_box=Entry(
        Point( int( (win_width*7/16) ) ,  int ( ( win_height*3/8) ) ),
        5)
    input11_box.setText(  str(transfer_matrix[1][1]))
    input11_box.draw(win)

    drawn_objects=[]
    drawn_objects.append(draw_picture(transfer_matrix, win) )




    # This is the main loop which draws the picture.  The picure is redrawn
    # with each click of the mouse, using the current values in the transform
    # matrix, until the user clicks on "quit"

    while(keep_open):
        clickPoint = win.getMouse()

        #if there is a valid click in a window execute the code below
        if (clickPoint):

            #if the user clicks on "quit" exit the program
            if (
                (clickPoint.getX() > -25) and
                (clickPoint.getX() < 25) and
                (clickPoint.getY() > int(  (win_height/-2) )    ) and
                (clickPoint.getY() < int( (win_height*-3/8))    ) ):
                keep_open = False

            #if the user clicks somewhere other than quit, do the following
            else:

                #remove the old drawing
                for objects in drawn_objects:
                    for element in objects:
                        element.undraw()
                    
                # try to read the elements in the transform matrix text boxes
                # and redraw the picture using the new values
                try:

                    transfer_matrix[0][0]=int( input00_box.getText() )
                    transfer_matrix[0][1]=int( input01_box.getText() )
                    transfer_matrix[1][0]=int( input10_box.getText() )
                    transfer_matrix[1][1]=int( input11_box.getText() )
                    drawn_objects.append (draw_picture(transfer_matrix, win))

                # if there is a problem with the read or draw operations,
                # do nothing and wait for the next mouse click. 
                except:
                    None  #this exception handler doesn't do anything


            
    win.close()


main()
