#RECIPE APP

Application for Recipes Users can create and manage recipes using the WPF application for Windows Presentation Foundation (WPF). In addition to performing various operations on the recipe data, 
it offers a graphical user interface (GUI) for entering recipe specifics, such as ingredients and procedures.
Users can create and manage recipes using the application as itt provides functionality to add ingredients, specify quantities, add steps,perform scaling on the recipe quantities and figuring out total calories. 
The application aims to assist users in managing and organizing their recipes efficiently.


##Installation Instructions

The procedures below need be followed to install and execute the Recipe Application WPF:

1. Make sure you have the right setup for running WPF apps, 
such Visual Studio or a different compatible development environment.
2. Download or clone the source code repository to your computer locally.
3. Open RecipeApplicationWPF.sln, the solution file, in the development environment of your choice.
4. To compile the code and handle any dependencies, build the solution.
5. Run the program from the development environment or create an executable file and run that.



##Usage Instructions

Follow these guidelines to utilize the Recipe Application WPF:

1. When the application has been installed successfully, run it.
2. Include the name of the ingredient, its calories, unit, quantity, and food group in the 
appropriate text areas.
3. To add an ingredient to the list of ingredients, click the "Add Ingredient" button.
4. A warning notice will appear if there are more than 350 calories inputted.
5. By typing each step in the "Step" text box and selecting "Add Step," you can add detailed directions for the recipe.
6. View the list of stages and additional ingredients in the corresponding list boxes.
7. In the "Recipe Name" text box, type the recipe's name.
8. To save the recipe with all of its ingredients and instructions, click the "Enter Recipe" button.
9. Enter a scaling ratio in the "Scaling" text box, then click the "Scaling" button to scale the 
ingredient and calorie amounts. The application will adjust the weights and calories as necessary.
10.Click the "Reset Quantities" button to reset all ingredient amounts and calories to zero.
11.Click the "Clear Recipe" option to start over after clearing the recipe. 
All of the stages, ingredients, and recipe name will be deleted as a result.
12.Click the "Exit" button to close the program.


##Class Structure
The Recipe Application WPF consists of the following classes:

MainWindow class: This class represents the main window of the application and handles user interactions,
such as adding ingredients and steps, displaying recipes, scaling quantities, and managing the GUI components.

Recipe class: This class represents a recipe object and contains properties for the recipe name, 
a list of ingredients, and a list of steps.

Ingredient class: This class represents an ingredient object and contains properties for the ingredient name, 
calories, unit, quantity, and food group.

The MainWindow class interacts with the Ingredient and Recipe classes to manage the recipe data and display it in the GUI.


##Method Explnation

When the "Add Ingredient" button is clicked by the user, the IngredientButton method is invoked. 
The ingredient data are retrieved, the input is verified, an Ingredient object is created, the ingredient is added to the list of ingredients, and the GUI is updated.

When a user clicks the "Add Step" button, the StepButton method is activated. 
The step is retrieved, added to the list of steps, and the GUI is updated.
[code]
// Example of adding a step
private void StepButton(object sender, RoutedEventArgs e)
{
    // Retrieve step text from text box
    string step = txtStep.Text;
    
    // Add step to the list
    steps.Add(step);
    
    // Update steps list box
    lstSteps.ItemsSource = steps;
    
    // Clear step field
    StepClearField();
}


The user clicks the "Display Recipe" button, which calls the method DisplayRecipeButton. 
The recipe's name, ingredients, and instructions are retrieved, the calories are totaled, and the recipe information is shown in a message box.

When the user presses the "Enter Recipe" button, the method EnterRecipeButton is invoked. 
It retrieves the ingredients, steps, and name of the recipe, then stores them in a Recipe object.
[code]
// Example of entering a recipe
private void EnterRecipeButton(object sender, RoutedEventArgs e)
{
    // Retrieve recipe name from text box
    string recipeName = txtRecipeName.Text;
    
    // Create recipe object with ingredients and steps
    Recipe recipe = new Recipe(recipeName, ingredients, steps);
    
    // Save the recipe
    
    // Clear recipe fields
    RecipeClearFields();
}


When a user presses the "Scaling" button, the ScaleButton function is triggered. 
In addition to updating the GUI, it retrieves the scaling factor and uses it to update the ingredient amounts and calories.
[code]
// Example of scaling ingredient quantities
private void ScalingButton(object sender, RoutedEventArgs e)
{
    // Retrieve scaling factor from text box
    string scalingFactorText = txtScalingFactor.Text;
    
    // Validate and apply scaling factor
    if (double.TryParse(scalingFactorText, out double scalingFactor))
    {
        if (scalingFactor > 0)
        {
            // Scale ingredient quantities and calories
            foreach (Ingredient ingredient in ingredients)
            {
                ingredient.Quantity *= scalingFactor;
                ingredient.Calories *= scalingFactor;
            }
            
            // Scale steps
            for (int i = 0; i < steps.Count; i++)
            {
                steps[i] = $"{i + 1}. {steps[i]}";
            }
            
            // Display scaled recipe information
            string recipeName = txtRecipeName.Text;
            string ingredientsInfo = string.Join(Environment.NewLine, ingredients.Select(i => $"{i.Name}: {i.Quantity} {i.Unit}"));
            string stepsInfo = string.Join(Environment.NewLine, steps);
            double totalCalories = ingredients.Sum(i => i.Calories);
            string recipeInfo = $"Scaled Recipe Name: {recipeName}" + Environment.NewLine +
                                $"Scaled Ingredients: {ingredientsInfo}" + Environment.NewLine +
                                $"Scaled Total Calories: {totalCalories}" + Environment.NewLine +
                                $"Scaled Steps: {stepsInfo}";
                                
            MessageBox.Show(recipeInfo, "Scaled Recipe");
        }
        else
        {
            MessageBox.Show( "Invalid Scaling Factor");
        }
    }
    else
    {
        MessageBox.Show("Invalid input for scaling factor. Please enter a valid number.");
    }
}


When the user hits the "Reset Quantities" button, this function is triggered. 
All ingredient quantities and calories are reset to zero, and the GUI is updated.

When the user clicks the "Clear Recipe" button, the ClearRecipeButton method is triggered. 
It changes the GUI and deletes the recipe name, ingredients, and steps.

When a user clicks the "Exit" button, this function is triggered. It terminates the program.


##Scaling Functionality

Users can modify component quantities and calories using the scaling functionality based on a scaling factor. 
The application increases the amounts and calories of all ingredients by the scaling factor when the user inputs a scaling factor and hits the "Scaling" button. 
Example: all amounts and calories will be doubled if the scaling factor is 2. 
The GUI then displays the modified settings.

##Program Execution

Observe these guidelines to run the Recipe Application WPF:

1. Use the produced executable file or build and execute the application from your development environment.
2. The Recipe Application WPF's main window will now display.
3. To use the program, adhere to the usage guidelines listed above.


##Formatting and Structure

The code follows standard C# formatting conventions, including proper indentation, descriptive variable and method names, and clear comments to 
enhance readability and maintainability.


##Error Handling

Error handling is built into the Recipe Application WPF to deal with incorrect input or mistakes.
An error warning will appear, for example, if the user enters a non-numeric value for calories or amount. 
Additionally, the application verifies the input to make sure that no ingredient has more than 350 calories. 
The application will give the user feedback and instructions on how to fix any faults if they arise.
