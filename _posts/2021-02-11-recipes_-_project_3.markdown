---
layout: post
title:      "Recipes - Project #3"
date:       2021-02-11 19:25:27 -0500
permalink:  recipes_-_project_3
---

For my Rails project at Flatiron School, I chose to build a Recipe Manger, which was one of the  example Domains for this project. After reading the requirements for the Domain, I immediately knew that this project would involve some complex nested forms and model associations. 
```
class Recipe
  has_many :recipe_ingredients
  has_many :ingredients, through: :recipe_ingredients
end

class Ingredient
  has many :recipe_ingredients
  has_many :recipes, through: :recipe_ingredients
end

class RecipeIngredient
  belongs_to :recipe
  belongs_to :ingredient
end
```
Nested forms are tricky, especially with a many to many relationship, and I will say that altough I struggled with the part, I am very glad I chose this domain, as I now feel much more confident on the subject.

Most of the process seemed pretty straightforward as I had been practicing a lot. So, I started planning out and slowly worked my way up to nested forms. This is where I got stuck!
While building a recipe, how do you allow users to create multiple ingredients on the same form? The first part, adding from a collection of ingredients that already exists was not hard, but creating multiple Ingredients on the same form and also creating new RecipeIngredients that associates with the recipe and the ingredient being created got really tricky and I soon found myself stuck in the weeds.

 My first approach was to allow users to create a recipe and add all the ingredients to it in one single form and in one single request. Again, this is the part where most of the complexity in this application lies. 
 First, I had to implement a way to build multiple blank ingredients and recipe_ingredients to be able to generate the form fields for them. Then, I had to build custom attributes= methods for both ingredients and recipe_ingredients as just having the ```accepts_nested_attributes_for``` macro was not sufficient in this case due to the many to many association between them. By the time I got to strong params, I was already very confused and as you can see the whole process for creating a recipe got very complicated.
 
 Next, after reserching online for solutions to this situation, I decided to try out a gem called "cocoon". Cocoon is a gem that makes it easier to handle nested forms. You can use it to dynamically generate and remove nested form fields.
This approach went along very well and I was able to generate multiple form fields for ingredients and also delete them on the same form. However, again, to add the quantity for the ingredients, I would need to add the recipe_ingredients fileds as well to the logic and this is where it starts to get complicated again. After trying multiple ways and spending a good amount of time trying to research for ideas  to solve this situation, I decided to move on and try a diffrent way.

My third approach to this problem was to break down the process of creating a recipe into two steps. 
1. First, the user creates a recipe with title, cook_time and instructions. Upon save, the user is redirected to the recipe show page. 
2. There, the user is provided a link to add ingredients and quantity to the recipe. Clicking the link will direct the  user to the new recipe_ingredient form and the user can add multiple ingredients to the recipe.
The code to achieve this in my RecipeIngredients controller looks like this:

```
# app/controllers/recipe_ingredients_controller.rb

def new
	if @recipe = Recipe.find_by(id: params[:recipe_id])
		@recipe_ingredient = @recipe.recipe_ingredients.build
		@recipe_ingredient.build_ingredient		
	end
end
	

def create
	@recipe_ingredient = RecipeIngredient.new(recipe_ingredient_params)	
	if @recipe_ingredient.save
		flash[:message] = "Sucessfully added ingredient. Add more or GO BACK!"
		redirect_to new_recipe_recipe_ingredient_path(@recipe_ingredient.recipe)
	else
		render :new
	end
end
		
	
```
Take a note here that after the recipe_ingredient is created, the user is redirected back to the new recipe_ingredient form with the option to add more than one ingredients before going back to the recipe.

The code in my recipe_ingredient.rb for assigning the attributes for ingredients  looks like this:

```
# app/models/recipe_ingredient.rb

def ingredient_attributes=(ingredient_attributes)
  self.ingredient = Ingredient.find_or_create_by(ingredient_attributes) if !ingredient_attributes['name'].blank?
end
```

And the strong params in my RecipeIngredients Controller:

```
# app/controllers/recipe_ingredients_controller.rb

def recipe_ingredient_params
  params.require(:recipe_ingredient).permit(:quantity, :recipe_id, :ingredient_id, ingredient_attributes: [:name])
end
```

This approach reduced the amount of code that I had to write significantly, and now all my files look clean. 
I am sure that there probably is a much better way of doing this with some javascript involved but that is out of the scope of this project.

The rest of the app building process went fairly smooth. This was a very good learning experience.
