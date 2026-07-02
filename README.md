import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class RadioButtonDemo extends JFrame {
    private JLabel imageLabel;
    private JRadioButton birdButton, catButton, dogButton, rabbitButton, pigButton;
    private ButtonGroup group;

    private final String birdImage = "bird.gif";
    private final String catImage = "cat.gif";
    private final String dogImage = "dog.gif";
    private final String rabbitImage = "rabbit.gif";
    private final String pigImage = "pig.gif";

    public RadioButtonDemo() {
        setTitle("RadioButtonDemo");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new BorderLayout(10, 10));

        birdButton = new JRadioButton("Bird");
        catButton = new JRadioButton("Cat");
        dogButton = new JRadioButton("Dog");
        rabbitButton = new JRadioButton("Rabbit");
        pigButton = new JRadioButton("Pig");

        group = new ButtonGroup();
        group.add(birdButton);
        group.add(catButton);
        group.add(dogButton);
        group.add(rabbitButton);
        group.add(pigButton);

        JPanel radioPanel = new JPanel();
        radioPanel.setLayout(new GridLayout(5, 1, 5, 5));
        radioPanel.setBorder(BorderFactory.createEmptyBorder(20, 20, 20, 10));
        radioPanel.add(birdButton);
        radioPanel.add(catButton);
        radioPanel.add(dogButton);
        radioPanel.add(rabbitButton);
        radioPanel.add(pigButton);

        imageLabel = new JLabel();
        imageLabel.setHorizontalAlignment(JLabel.CENTER);
        imageLabel.setBorder(BorderFactory.createEmptyBorder(20, 10, 20, 20));

        pigButton.setSelected(true);
        updateImage(pigImage);

        ActionListener listener = new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                JRadioButton source = (JRadioButton) e.getSource();
                String petName = source.getText();

                JOptionPane.showMessageDialog(RadioButtonDemo.this,
                        "You selected: " + petName,
                        "Pet Selection",
                        JOptionPane.INFORMATION_MESSAGE);

                if (source == birdButton) updateImage(birdImage);
                else if (source == catButton) updateImage(catImage);
                else if (source == dogButton) updateImage(dogImage);
                else if (source == rabbitButton) updateImage(rabbitImage);
                else if (source == pigButton) updateImage(pigImage);
            }
        };

        birdButton.addActionListener(listener);
        catButton.addActionListener(listener);
        dogButton.addActionListener(listener);
        rabbitButton.addActionListener(listener);
        pigButton.addActionListener(listener);

        add(radioPanel, BorderLayout.WEST);
        add(imageLabel, BorderLayout.CENTER);

        setSize(450, 250);
        setLocationRelativeTo(null);
        setVisible(true);
    }

    private void updateImage(String filename) {
        try {
            ImageIcon icon = new ImageIcon(filename);
            Image img = icon.getImage();
            Image scaledImg = img.getScaledInstance(180, 150, Image.SCALE_SMOOTH);
            imageLabel.setIcon(new ImageIcon(scaledImg));
        } catch (Exception ex) {
            imageLabel.setText("Image not found: " + filename);
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            @Override
            public void run() {
                new RadioButtonDemo();
            }
        });
    }
}
