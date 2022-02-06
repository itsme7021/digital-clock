// digital-clock
//digital clock made using java swing

we are gonna make two java classes in the package, one is the main class and other is the window.
Main class calls the constructor of the window class.
Window class is where the main code is written.
Necessary packages are imported.
Then we make the constructor where the we make the frame and set its name, location, etc... and there we also called the createGui method(which is declared later) followed by startClock method
In the createGui method we created the headings, layout, etc
In the startClock method using multithreading we are gonna call for the current time every 1000 milliseconds
so that it appears like it is a digital clock, but in real it is only method calling for the current time and date every 1000 milliseconds

CODE 

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.text.SimpleDateFormat;
import java.util.Date;

public class window extends JFrame {
    private JLabel heading;
    private JLabel clocklabel;
    private Font font = new Font("" , Font.BOLD , 36); //takes three input font family ,boldness etc and size
    window()
    {
        super.setTitle("My clock");
        super.setSize(400 , 400); //sets size of the window
        super.setLocation(300 , 60); //sets location i.e where on the scree the window will pop open
        super.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE); //this will stop the program as soon as we close the window
        createGui();
        startClock();
        super.setVisible(true);  //sets the visibility of the window
    }

    public void createGui()
    {
        heading = new JLabel("My clock");
        clocklabel = new JLabel("Clock");

        heading.setFont(font);
        clocklabel.setFont(font);

        this.setLayout(new GridLayout(2 , 1));  //this sets the layout of the window into grid

        this.add(heading);
        this.add(clocklabel);
    }

    public void startClock()
    {
        /*//we are gonna use the timer class the timer class calls the action performed method after a decided interval
        // actionPerformed method is in interface actionListener()
        Timer t = new Timer(1000, new ActionListener() {    //here takes input in milliseconds ,anonymous class is called
            @Override
            public void actionPerformed(ActionEvent e) {
                //String Dt = new Date().toString();
                //String Dt = new Date().toLocaleString();
                Date d = new Date();
                SimpleDateFormat sf = new SimpleDateFormat("hh : mm : ss a -  - Y");  //hh mm ss are specifiers we can also look at oracle website for more
                String Dt = sf.format(d);
                clocklabel.setText(Dt);
            }
        });

        t.start();  //starts the timer class
         */

        //by threading

        Thread th = new Thread(){
            public void run()
            {
                try {
                    //String Dt = new Date().toString();
                    //String Dt = new Date().toLocaleString();
                    Date d = new Date();
                    SimpleDateFormat sf = new SimpleDateFormat("hh : mm : ss a - Y");  //hh mm ss are specifiers we can also look at oracle website for more
                    String Dt = sf.format(d);
                    clocklabel.setText(Dt);

                    Thread.sleep(1000);
                }
                catch (InterruptedException e)
                {
                    e.getStackTrace();
                }
            }
        };
        th.start();
    }
}
