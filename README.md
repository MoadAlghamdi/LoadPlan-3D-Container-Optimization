
# LoadPlan — Automated Container Load Optimization

A browser-based application for planning and visualizing cargo placement inside containers. LoadPlan combines a constraint-based 3D packing heuristic with a genetic algorithm that searches for better cargo loading orders.

The project explores how optimization and interactive visualization can support logistics planning across sea, road, rail, and air transport.

## Overview

Container loading involves more than fitting boxes into an available space. A loading plan must also consider payload limits, cargo orientation, fragile items, stacking restrictions, and unloading destinations.

LoadPlan allows users to enter or import cargo data, generate loading plans, inspect placements in 3D, and compare alternative planning objectives.

## Key Features

* **Interactive 3D visualization:** Inspect cargo placement and view loading steps.
* **Cargo input:** Enter cargo manually or import a CSV file.
* **Multiple transport modes:** Select container presets for sea, road, rail, and air transport.
* **Constraint-based packing:** Consider container boundaries, overlap, payload, orientation, door dimensions, stacking limits, and base support.
* **Fragile cargo handling:** Prevent items from being stacked on fragile or non-stackable cargo.
* **Destination grouping:** Use destination information to guide loading placement.
* **Multi-container planning:** Distribute cargo across an available container fleet.
* **Shipment strategies:** Choose from strategies targeting fewer containers, higher utilization, lower cost, or a specified fleet order.
* **Genetic algorithm optimization:** Search alternative cargo-type orderings to improve the selected objective.
* **Scenario comparison:** Compare packing objectives and inspect their results.
* **Loading manifests and exports:** Review loading sequences and export planning data.
* **Load metrics:** Track volume utilization, payload utilization, packed pieces, and center-of-gravity offsets.
* **Rejected cargo explanations:** Review why items could not be placed.

## How It Works

### 1. Define the shipment

Enter cargo dimensions, weight, quantity, handling restrictions, priority, and destination. Select a container or configure a fleet.

### 2. Generate a packing plan

The packing engine evaluates available spaces and allowed orientations. It checks modeled constraints before scoring feasible placements.

### 3. Optimize the loading order

The genetic algorithm represents each candidate as an ordering of cargo types. It evaluates candidates using the packing engine, then applies selection, crossover, and mutation to search for improved plans.

### 4. Inspect and export

Explore the result in 3D, review loading steps and rejected cargo, compare scenarios, and export the plan.

## Technology Stack

* HTML5
* CSS3
* JavaScript
* Three.js
* Web Workers for background optimization, where supported
* Browser File APIs for CSV import and export

The application runs in the browser and does not require a backend server.

## Getting Started

1. Download or clone this repository.
2. Open `index.html` in a modern browser.
3. Select a transport mode and container.
4. Enter cargo manually or import a CSV file.
5. Generate a packing plan.
6. Run the optimizer or compare scenarios.
7. Inspect the 3D loading plan and export the results.

An internet connection is required to load the externally hosted Three.js library and Google Fonts.

## Cargo CSV Format

The cargo importer supports the following column names:

`name,length_cm,width_cm,height_cm,weight_kg,qty,fragile,stackable,tip,max_load_kg,priority,destination`

* Dimensions are measured in centimeters.
* Weight and maximum supported load are measured in kilograms.
* `fragile` indicates whether cargo must not support other items.
* `stackable` indicates whether other items may rest on the cargo.
* `tip` indicates whether the cargo may be placed on its side.
* `priority` sets loading priority from 1 to 5.
* `destination` identifies the unloading stop.

## Scope and Limitations

LoadPlan is an academic planning prototype. Its heuristic and genetic algorithm approaches do not guarantee a globally optimal solution.

The current model treats cargo as rectangular boxes and approximates contoured air containers using stepped blocked volumes. Base support is evaluated using contact area, with a 75% threshold.

The application does not currently model axle loads, load securing, hazardous-material segregation, aircraft trim, or full physical stability. Center-of-gravity metrics support inspection but do not enforce a hard balance constraint.

Default freight costs are illustrative and should be replaced with shipment-specific quotations before evaluating cost-based plans.

## Future Improvements

* Benchmark packing quality and execution time on documented datasets.
* Add axle-load and center-of-mass support constraints.
* Introduce category-based cargo segregation.
* Support expiry-aware unloading priorities.
* Improve modeling of irregular cargo.
* Extend automated validation of packing constraints.

## Project Context

Developed as a graduation project in Artificial Intelligence at the University of Jeddah, exploring optimization methods and 3D visualization for logistics planning.
