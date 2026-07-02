import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

/**
 * RadioButtonDemo
 * A simple Swing application with 5 radio buttons to choose a pet.
 * Selecting a pet shows its picture and pops up a message box with the choice.
 *
 * Expects an "images" folder (containing bird.png, cat.png, dog.png,
 * rabbit.png, pig.png) marked as a Resources Root, sitting next to "src".
 */
public class RadioButtonDemo extends JFrame implements ActionListener {

    private JRadioButton birdButton, catButton, dogButton, rabbitButton, pigButton;
    private JLabel petLabel;

    public RadioButtonDemo() {
        setTitle("RadioButtonDemo");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new BorderLayout(10, 10));

        // ---- Radio buttons panel ----
        birdButton   = new JRadioButton("Bird");
        catButton    = new JRadioButton("Cat");
        dogButton    = new JRadioButton("Dog");
        rabbitButton = new JRadioButton("Rabbit");
        pigButton    = new JRadioButton("Pig");

        ButtonGroup group = new ButtonGroup();
        group.add(birdButton);
        group.add(catButton);
        group.add(dogButton);
        group.add(rabbitButton);
        group.add(pigButton);

        birdButton.addActionListener(this);
        catButton.addActionListener(this);
        dogButton.addActionListener(this);
        rabbitButton.addActionListener(this);
        pigButton.addActionListener(this);

        JPanel radioPanel = new JPanel();
        radioPanel.setLayout(new BoxLayout(radioPanel, BoxLayout.Y_AXIS));
        radioPanel.setBorder(BorderFactory.createEmptyBorder(20, 20, 20, 20));
        radioPanel.add(birdButton);
        radioPanel.add(catButton);
        radioPanel.add(dogButton);
        radioPanel.add(rabbitButton);
        radioPanel.add(pigButton);

        // ---- Picture label ----
        petLabel = new JLabel("Select a pet", SwingConstants.CENTER);
        petLabel.setPreferredSize(new Dimension(260, 260));
        petLabel.setBorder(BorderFactory.createLineBorder(Color.GRAY));
        petLabel.setHorizontalAlignment(SwingConstants.CENTER);

        add(radioPanel, BorderLayout.WEST);
        add(petLabel, BorderLayout.CENTER);

        pack();
        setLocationRelativeTo(null);
    }

    /** Loads an image from the images/ folder (relative to project root) and shows it. */
    private void showImage(String fileName) {
        String path = "images/" + fileName;
        ImageIcon icon = new ImageIcon(path);
        if (icon.getIconWidth() > 0) {
            petLabel.setIcon(icon);
            petLabel.setText(null);
        } else {
            petLabel.setIcon(null);
            petLabel.setText("Image not found: " + path);
        }
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        String pet;

        if (e.getSource() == birdButton) {
            pet = "Bird";
            showImage("bird.png");
        } else if (e.getSource() == catButton) {
            pet = "Cat";
            showImage("cat.png");
        } else if (e.getSource() == dogButton) {
            pet = "Dog";
            showImage("dog.png");
        } else if (e.getSource() == rabbitButton) {
            pet = "Rabbit";
            showImage("rabbit.png");
        } else {
            pet = "Pig";
            showImage("pig.png");
        }

        JOptionPane.showMessageDialog(this, "You selected: " + pet,
                "Your Choice", JOptionPane.INFORMATION_MESSAGE);
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            RadioButtonDemo frame = new RadioButtonDemo();
            frame.setVisible(true);
        });
    }
}
