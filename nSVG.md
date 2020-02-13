# Scalable Vector Graphics SVG

https://github.com/webdetails/Viz-SVG

Summarized, visualizations are composed of:

- a generic model, that all new visualizations extend from (javascript file)
- a config file to register current available visualizations (js file)
- a view to control the SVG rendering (js file)
- and, a specific model (js file), representing the visualization,  that extends the generic model and implements the actual visualizaion  logic.

To create a new visualization one must:

- get an SVG that represents the needed visualization (paint the SVG  elements that you will change in gray, or another neutral color, to  create the change perception)
- create a model with the business logic used to change the SVG
- and, register the new model on config.js