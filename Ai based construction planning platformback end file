from flask import Flask, render_template, request

app = Flask(__name__)


def generate_plan(project, area, budget, location, floors):
    area = float(area)
    budget = float(budget)
    floors = int(floors)

    total_builtup_area = area * floors

    # MATERIAL ESTIMATION
    bricks = int(total_builtup_area * 8)
    cement_bags = int(total_builtup_area * 0.4)
    sand_tons = round(total_builtup_area * 0.05, 2)
    steel_kg = int(total_builtup_area * 4)
    aggregate_tons = round(total_builtup_area * 0.06, 2)
    flooring_sqft = total_builtup_area
    paint_liters = round(total_builtup_area * 0.18, 2)
    electrical_wire_m = int(total_builtup_area * 1.5)
    tiles_boxes = int(total_builtup_area / 15)

    # MATERIAL COSTS (approx demo values)
    brick_cost = bricks * 8
    cement_cost = cement_bags * 420
    sand_cost = sand_tons * 1500
    steel_cost = steel_kg * 65
    aggregate_cost = aggregate_tons * 1200
    tiles_cost = flooring_sqft * 60
    paint_cost = paint_liters * 300
    electrical_cost = electrical_wire_m * 120

    estimated_cost = int(
        brick_cost
        + cement_cost
        + sand_cost
        + steel_cost
        + aggregate_cost
        + tiles_cost
        + paint_cost
        + electrical_cost
    )

    # Budget comparison
    if estimated_cost > budget:
        budget_status = "Budget is LOWER than estimated cost"
    else:
        budget_status = "Budget is sufficient"

    result = f"""
Construction Plan for {project}

Location: {location}
Plot Area: {area} sq ft
Number of Floors: {floors}
Total Built-up Area: {total_builtup_area} sq ft

Your Budget: ₹{budget:,.0f}
Estimated Construction Cost: ₹{estimated_cost:,.0f}

Budget Analysis:
{budget_status}

Estimated Materials Required:

1. Bricks: {bricks}
2. Cement Bags: {cement_bags}
3. Sand: {sand_tons} tons
4. Steel: {steel_kg} kg
5. Aggregate: {aggregate_tons} tons
6. Flooring/Tiles Area: {flooring_sqft} sq ft
7. Paint Required: {paint_liters} liters
8. Electrical Wiring: {electrical_wire_m} meters
9. Tiles Boxes: {tiles_boxes}

Construction Steps:
1. Site preparation
2. Foundation work
3. Column and beam work
4. Slab casting
5. Wall construction
6. Electrical & plumbing
7. Flooring
8. Painting & finishing

Note:
Estimated cost is calculated based on approximate market prices.
Actual cost may vary depending on location, contractor, and design.
"""
    return result


@app.route("/", methods=["GET", "POST"])
def index():
    result = ""

    if request.method == "POST":
        project = request.form["project"]
        area = request.form["area"]
        budget = request.form["budget"]
        location = request.form["location"]
        floors = request.form["floors"]

        result = generate_plan(project, area, budget, location, floors)

    return render_template("index.html", result=result)


if __name__ == "__main__":
    app.run(debug=True)
