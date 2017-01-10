# JApplet-fun
Simple code for an applet

package eyesfollow;

import javax.swing.JApplet;
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;
import java.awt.event.MouseEvent;
import java.awt.event.MouseMotionListener;

public class EyesFollow extends JApplet implements MouseListener {
    
    // boolean to check if mouse is inside applet window
    boolean mouseEntered;
    // used to track mouse movement
    private int mxpos;
    private int mypos;
    // positions of eyeballs 1 and 2
    private int ball1X = 155;
    private int ball2X = 185;
    private int ball1Y = 100;
    private int ball2Y = 100;
    // boundaries for eyeball 1
    private final int maxX1 = 160;
    private final int minX1 = 150;
    private final int maxY1 = 110;
    private final int minY1 = 90;
    // boundaries for eyeball 2
    private final int maxX2 = 190;
    private final int minX2 = 180;
    private final int maxY2 = 110;
    private final int minY2 = 90;
    
    // time delay
    private final int TIME_DELAY = 1;
    // amount of pixels the eyeballs move
    private final int MOVE = 1;
    // timer
    private Timer timer;
    
    public void init() {
        //adds timer to the class
        timer = new Timer(TIME_DELAY, new TimerListener());
        timer.start();
        // adds mouse listener and motion listener to panel
        addMouseListener(this);  
        addMouseMotionListener(new MyMouseMotionListener());
        
    }
    
    public void paint(Graphics g) {
        
        super.paint(g);
        // Draws ovals for eyes 
        g.drawOval(150, 90, 20, 30);
        
        g.drawOval(180, 90, 20, 30);
        // draws filled ovals for eyeballs
        g.fillOval(ball1X, ball1Y, 10, 10);
        
        g.fillOval(ball2X, ball2Y, 10, 10);
        
        // prints location and message if mouse is in applet and outside applet
        if (mouseEntered) g.drawString("(" + mxpos + "," + mypos + ")", 20, 160);
        if (mouseEntered) g.drawString("Mouse is in the applet area",20,180); 
        else g.drawString("Mouse is outside the Applet area",20,180); 
        
       
 }

    private class MyMouseMotionListener implements MouseMotionListener {
    
        public void mouseDragged(MouseEvent e) {
                        
        }
        // stores location of mouse
    public void mouseMoved(MouseEvent e) {
        
        if (mouseEntered == true)
        
            mxpos = e.getX();
            mypos = e.getY();
            
        }
    }
    
    
    public void mouseEntered(MouseEvent e) {
        
        mouseEntered = true;
        
        
    }
    // returns false and places eyeballs to original position
    public void mouseExited(MouseEvent e) {
        
        mouseEntered = false;
        
        ball1X = 155;
        ball1Y = 100;
        
        ball2X = 185;
        ball2Y = 100;
                
        repaint();
        
    }

    
    public void mouseClicked(MouseEvent me) {
    
    }

    
    public void mousePressed(MouseEvent me) {
    
    }

   
    public void mouseReleased(MouseEvent me) {
    }

    

    
private class TimerListener implements ActionListener {
        
        public void actionPerformed(ActionEvent e) {
            
            if (mouseEntered == true) {
                //X Direction Right
                if (mxpos > ball1X)                    
                    ball1X += MOVE;
                //X Direction Max Right
                if (ball1X > maxX1)                    
                    ball1X -= MOVE;
                //X Direction Left
                if (mxpos < ball1X)
                    ball1X -= MOVE;
                //X Direction Max Left
                if (ball1X < minX1) 
                    ball1X += MOVE;
                
                // Y Direction Down
                if (mypos > ball1Y)
                    ball1Y += MOVE;
                // Y Direction Max Down
                if (ball1Y > maxY1)
                    ball1Y -= MOVE;
                // Y Direction Up 
                if (mypos < ball1Y)
                    ball1Y -= MOVE;
                // Y Direction Max Up
                if (ball1Y < minY1)
                    ball1Y += MOVE;
                
                // Right Eye
                
                //X Direction Right
                if (mxpos > ball2X)                    
                    ball2X += MOVE;
                //X Direction Max Right
                if (ball2X >= maxX2)                    
                    ball2X -= MOVE;
                //X Direction Left
                if (mxpos < ball2X)
                    ball2X -= MOVE;
                //X Direction Max Left
                if (ball2X <= minX2) 
                    ball2X += MOVE;
                
                // Y Direction Down
                if (mypos > ball2Y)
                    ball2Y += MOVE;
                // Y Direction Max Down
                if (ball2Y >= maxY2)
                    ball2Y -= MOVE;
                // Y Direction Up 
                if (mypos < ball2Y)
                    ball2Y -= MOVE;
                // Y Direction Max Up
                if (ball2Y <= minY2)
                    ball2Y += MOVE;
                
                repaint();
                
            }
            
        }

    }


public static void main(String[] args) {

new EyesFollow();

}
}
