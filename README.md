import javafx.application.Application;
import javafx.fxml.FXMLLoader;
import javafx.scene.Parent;
import javafx.scene.Scene;
import javafx.stage.Stage;
import javafx.scene.control.TextField;

public class Main extends Application {

    public static void main(String[] args) {
        launch(args);
    }

    @Override
    public void start(Stage primaryStage) throws Exception {
        Parent root = FXMLLoader.load(getClass().getResource("Main.fxml"));
        primaryStage.setTitle("Formatador de CPF");
        primaryStage.setScene(new Scene(root, 300, 200));
        primaryStage.show();
    }

    public void initialize() {
        TextField cpfField = new TextField();
        TextField formattedCpfField = new TextField();
        formattedCpfField.setEditable(false);

        cpfField.textProperty().addListener((observable, oldValue, newValue) -> {
            String formattedCPF = formatCPF(newValue);
            formattedCpfField.setText(formattedCPF);
        });
    }

    private String formatCPF(String value) {
        // Remove all non-digit characters from the input string
        String digitsOnly = value.replaceAll("\\D", "");

        // Format the CPF with dots and dashes
        StringBuilder formattedCPF = new StringBuilder();
        for (int i = 0; i < Math.min(digitsOnly.length(), 11); i++) {
            formattedCPF.append(digitsOnly.charAt(i));
            if (i == 2 || i == 5) {
                formattedCPF.append(".");
            } else if (i == 8) {
                formattedCPF.append("-");
            }
        }
        return formattedCPF.toString();
    }
}


<!-- Main.fxml -->
<?xml version="1.0" encoding="UTF-8"?>

<?import javafx.scene.layout.VBox?>
<?import javafx.scene.control.TextField?>

<VBox alignment="CENTER" spacing="10" xmlns="http://javafx.com/javafx/11.0.1"
      xmlns:fx="http://javafx.com/fxml/1">
    <TextField fx:id="cpfField" promptText="Digite o CPF"/>
    <TextField fx:id="formattedCpfField" promptText="CPF formatado" editable="false"/>
</VBox>
