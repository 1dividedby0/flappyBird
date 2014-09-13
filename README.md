flappyBird
==========

flappyBird recreation using acm.graphics libraries
I love to code

import java.awt.event.KeyEvent;

import acm.graphics.GImage;
import acm.graphics.GLabel;
import acm.graphics.GLine;
import acm.graphics.GObject;
import acm.graphics.GRect;
import acm.program.GraphicsProgram;
import acm.util.RandomGenerator;
import acmx.export.javax.swing.JLabel;

public class main1 extends GraphicsProgram {
	static GImage flappyBird = new GImage("flappyBird.jpg");

	private static int APPLICATION_WIDTH = 500;
	private static int APPLICATION_HEIGHT = 400;
	int i = APPLICATION_WIDTH + 255;
	private int vy;
	private int tubeSpeed = 10;

	GLine gravity;
	GLabel gameOver = new GLabel("Game Over");
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		new main1().start();
	}

	public void run() {
		addKeyListeners();
		GImage wall = new GImage("flappyPipe.jpeg");
		flappyBird.setSize(60, 50);
		RandomGenerator randYe = new RandomGenerator();
		int randY = randYe.nextInt(APPLICATION_HEIGHT);
		if (randY > (250)) {
			randY -= 150;
		}
		if (randY > 300) {
			randY -= 150;
		}
		add(flappyBird);
		add(wall);
		wall.setLocation(i, randY);
		
		while (true) {
			wall.setSize(70, 150);
			pause(tubeSpeed);
			
			wall.move(-1, 0);
			pause(tubeSpeed);
			flappyBird.move(0, vy);
			if ((wall.getX() + 70) < 0) {
				RandomGenerator ye = new RandomGenerator();
				int y = ye.nextInt(APPLICATION_HEIGHT) - 99;
				wall.setLocation(i, y);
				if (y > (300)) {
					// y -= 150;
					System.out.println("invalid");
				}
				if (y > 400) {
					// y -= 150;
					System.out.println("invalid");
				}

			}
			if(collision(flappyBird, wall)){
				vy=0;
				wall.move(0, 0);
				wall.setLocation(wall.getX(), wall.getY());
				gameOver.setVisible(true);
				add(gameOver);
				pause(1000000000);
				
				
			}
		}
		
	}

	public void keyPressed(KeyEvent ke) {
		if (ke.getKeyCode() == KeyEvent.VK_DOWN) {
			vy = 2;
			
		}
		if (ke.getKeyCode() == KeyEvent.VK_UP) {
			vy = -2;
			add(gravity);
			double b = flappyBird.getY();
			gravity = new GLine(flappyBird.getX(),b-10, flappyBird.getX(),b-10 );
			gravity.setLocation(flappyBird.getX(), b-10);
			if(collision(flappyBird, gravity)){
				vy=2;
			}
			
			
		}
	}
	public boolean collision(GObject a, GObject b)

	{

		if (a.getBounds().intersects(b.getBounds())) {

			return true;

		}

		else {

			return false;

		}

	}

}
