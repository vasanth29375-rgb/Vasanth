import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class SimplePlaylistApp extends JFrame {

    private DefaultListModel<String> playlistModel;
    private JList<String> playlistJList;
    private JTextField songInputField;

    public SimplePlaylistApp() {
        // 1. Setup the Main Window (JFrame)
        setTitle("Simple Music Playlist");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setSize(400, 500);
        setLayout(new BorderLayout(10, 10)); // Use BorderLayout for main layout
        
        // 2. Initialize Playlist Data Model and List
        playlistModel = new DefaultListModel<>();
        // Add some initial songs to simulate a current playlist
        playlistModel.addElement("Blinding Lights - The Weeknd");
        playlistModel.addElement("Bohemian Rhapsody - Queen");
        playlistModel.addElement("Uptown Funk - Mark Ronson ft. Bruno Mars");
        
        playlistJList = new JList<>(playlistModel);
        playlistJList.setFont(new Font("SansSerif", Font.PLAIN, 14));
        // Wrap the JList in a JScrollPane to handle many songs
        JScrollPane scrollPane = new JScrollPane(playlistJList);

        // 3. Create the Control Panel (Buttons and Input)
        JPanel controlPanel = new JPanel();
        controlPanel.setLayout(new FlowLayout(FlowLayout.CENTER, 10, 10)); // Layout for controls

        songInputField = new JTextField(20);
        
        JButton addButton = new JButton("Add Song");
        JButton removeButton = new JButton("Remove Selected");

        // 4. Add Action Listeners for Functionality
        
        // Add Song Functionality
        addButton.addActionListener(e -> {
            String newSong = songInputField.getText().trim();
            if (!newSong.isEmpty()) {
                playlistModel.addElement(newSong);
                songInputField.setText(""); // Clear the input field
            } else {
                JOptionPane.showMessageDialog(this, 
                    "Please enter a song name.", "Input Error", JOptionPane.WARNING_MESSAGE);
            }
        });

        // Remove Selected Song Functionality
        removeButton.addActionListener(e -> {
            int selectedIndex = playlistJList.getSelectedIndex();
            if (selectedIndex != -1) { // Check if an item is actually selected
                playlistModel.remove(selectedIndex);
            } else {
                 JOptionPane.showMessageDialog(this, 
                    "Please select a song to remove.", "Selection Error", JOptionPane.WARNING_MESSAGE);
            }
        });
        
        // Add components to the control panel
        controlPanel.add(new JLabel("Song Title:"));
        controlPanel.add(songInputField);
        controlPanel.add(addButton);
        controlPanel.add(removeButton);

        // 5. Place Components into the Main Frame
        
        // Add the scrollable playlist list to the center
        add(scrollPane, BorderLayout.CENTER);
        
        // Add the controls to the bottom
        add(controlPanel, BorderLayout.SOUTH); 
        
        // Make the window visible
        setVisible(true);
    }

    public static void main(String[] args) {
        // Run the GUI creation on the Event Dispatch Thread (safe Swing practice)
        SwingUtilities.invokeLater(SimplePlaylistApp::new);
    }
}# Vasanth
