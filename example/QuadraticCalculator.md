```xml
<?xml version="1.0" encoding="UTF-8"?>

<?import java.lang.*?>
<?import java.util.*?>
<?import javafx.scene.*?>
<?import javafx.scene.control.*?>
<?import javafx.scene.layout.*?>
<?import javafx.geometry.Insets?>

<VBox xmlns:fx="http://javafx.com/fxml/1" fx:controller="quadraticcalculator.FXMLDocumentController">
    <GridPane >
        <columnConstraints>
            <ColumnConstraints percentWidth="25.0" />
            <ColumnConstraints percentWidth="75.0" />
        </columnConstraints>
        <children>
            <Label text="Quadratic Equation Solver" GridPane.halignment="CENTER" GridPane.rowIndex="0" GridPane.columnIndex="0" GridPane.columnSpan="2" />
            <Label text="A Value:" GridPane.halignment="RIGHT" GridPane.rowIndex="1" GridPane.columnIndex="0" />
            <TextField GridPane.rowIndex="1" GridPane.columnIndex="1" GridPane.columnSpan = "1" fx:id="aval"/>
            <Label text="B Value:" GridPane.halignment="RIGHT" GridPane.rowIndex="2" GridPane.columnIndex="0" />
            <TextField GridPane.rowIndex="2" GridPane.columnIndex="1" GridPane.columnSpan="1" fx:id="bval"/>
            <Label text="C Value:" GridPane.halignment="RIGHT" GridPane.rowIndex="3" GridPane.columnIndex="0" />
            <TextField GridPane.rowIndex="3" GridPane.columnIndex="1" GridPane.columnSpan="1" fx:id="cval"/>
        </children>
    </GridPane>
    <HBox alignment="CENTER">
        <Button text="_Solve" onAction="#solve" mnemonicParsing="true" defaultButton="true">
            <HBox.margin>
                <Insets top="5.0" bottom="5.0" left="5.0" right="5.0" />
            </HBox.margin>
        </Button>
        <Button text="_Clear" onAction="#clear" mnemonicParsing="true" cancelButton="true" >
            <HBox.margin>
                <Insets top="5.0" bottom="5.0" left="5.0" right="5.0" />
            </HBox.margin>
        </Button>
    </HBox>
    <Label fx:id="solution" />
</VBox>
```
```java
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package quadraticcalculator;

import java.net.URL;
import java.util.ResourceBundle;
import javafx.event.ActionEvent;
import javafx.fxml.FXML;
import javafx.fxml.Initializable;
import javafx.scene.control.Label;
import javafx.scene.control.TextField;

/**
 *
 * @author sehyu
 */
public class FXMLDocumentController implements Initializable {

    @FXML
    private Label solution;

    @FXML
    private TextField aval, bval, cval;

    @FXML
    private void solve(ActionEvent event) {
        double a = Double.parseDouble(aval.getText());
        double b = Double.parseDouble(bval.getText());
        double c = Double.parseDouble(cval.getText());

        double discriminant = Math.pow(b, 2) - 4 * a * c;
        double first, second;

        if (discriminant == 0) {
            first = (-b + Math.sqrt(discriminant)) / (2 * a);
            solution.setText(String.format("Solution: x=%.2f", first));
        } else if (discriminant > 0) {
            first = (-b + Math.sqrt(discriminant)) / (2 * a);
            second = (-b - Math.sqrt(discriminant)) / (2 * a);
            solution.setText(String.format("Solution: x=%.2f y=%.2f", first, second));
        } else {
            solution.setText("Solution: No Solution");
        }
    }

    @FXML
    private void clear(ActionEvent event) {
        aval.setText("");
        bval.setText("");
        cval.setText("");
    }

    @Override
    public void initialize(URL url, ResourceBundle rb) {
        // TODO
    }

}
```
```java
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package quadraticcalculator;

import javafx.application.Application;
import javafx.fxml.FXMLLoader;
import javafx.scene.Parent;
import javafx.scene.Scene;
import javafx.stage.Stage;

/**
 *
 * @author sehyu
 */
public class QuadraticCalculator extends Application {
    
    @Override
    public void start(Stage stage) throws Exception {
        Parent root = FXMLLoader.load(getClass().getResource("FXMLDocument.fxml"));
        stage.setTitle("Calculator");
        Scene scene = new Scene(root);
        
        stage.setScene(scene);
        stage.show();
    }

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {
        launch(args);
    }
    
}
```
![QudraticCalculator](images/QudraticCalculator.png)