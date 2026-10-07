# Interactive Dashboard: Furniture Inventory by Room

## 1. Project Overview

This project is an interactive Power BI dashboard that shows a home's furniture inventory on top of a floor plan. Each room on the plan is a clickable, color-coded area linked to the inventory data, so users can see what is in a room by selecting it on the map instead of searching through a list.

* **Use case:** Room-by-room inventory tracking for a residential property
* **Intended audience:** Homeowners, property or facilities staff, movers, or anyone who needs a quick spatial view of household assets
* **Main technologies:** Microsoft Power BI Desktop, with a custom image-map visual that turns floor plan regions into interactive data points

## 2. Business Problem & Objectives

### Problem

Inventory lists are usually kept as flat tables. A table can tell you that there are six chairs in the dining room, but it does not show where things are or make it easy to compare rooms at a glance. Finding everything in a single room means scanning or filtering rows by hand.

### Objectives

* Present the furniture inventory in a visual, location-based format
* Let users explore inventory by room with a single click
* Keep a detailed item list and an overall total visible next to the map
* Make the data easy to read for non-technical users

## 3. Solution

The dashboard has two linked visuals on one report page:

* **Interactive Areas:** A floor plan image where each room (Eat-in Kitchen, Formal Living, Formal Dining, Family, Entrance, 1/2 Bath, Laundry/Storage) is a mapped, color-coded region bound to the `Room` field
* **No of furniture:** A table listing each furniture type, its quantity and its room, with a grand total of 38 items

### End-to-End Workflow

1. Inventory data (furniture type, quantity, room) is loaded into the Power BI data model.
2. Floor plan regions are mapped to room values so each area on the image represents one room.
3. The user hovers over a room to see a tooltip with the room name and total item count (for example, Kitchen: 8).
4. The user clicks a room, and the table filters to show only that room's items and subtotal.
5. The user selects a row in the table, and the matching room is highlighted on the floor plan.
6. Clearing the selection returns the dashboard to the full inventory view.

## 4. Solution Architecture & Technologies

| Component | Role |
|---|---|
| **Power BI Desktop** | Report authoring, data model and interactive report page |
| **Custom image-map visual** | Displays the floor plan and binds each room shape to inventory data. The on-canvas toolbar (Change, Gallery, zoom controls) is consistent with the Synoptic Panel custom visual. |
| **Table visual** | Shows furniture, quantity and room with a total row, sorted by quantity |
| **Power BI cross-filtering** | Links the map and table so a selection in either visual filters or highlights the other |
| **Tooltips** | Show room name and summed quantity on hover |

```
Inventory data (Furniture, Quantity, Room)
            │
            ▼
   Power BI data model
            │
   ┌────────┴─────────┐
   ▼                  ▼
Floor plan map   ◄──►  Furniture table
(rooms as regions)    (items, quantity, total)
        cross-filtering by Room
```

The original data source is not shown in the demonstration.

## 5. Controls & Validation

This is a reporting and visualization project, so it does not include data entry, approvals or exception handling. The controls that are demonstrated are:

* **Consistent aggregation:** Quantities are summed per room and per item, and the total updates to match the current selection (for example, 38 overall, 8 for the Kitchen)
* **Two-way filtering:** Map and table stay in sync, which keeps the room view and the item list consistent
* **Visual state cues:** Unselected rooms are dimmed and the selected room is highlighted, so the active filter is always clear

## 6. Business Value

* **Better visibility:** Inventory is shown in its physical context, not just as rows in a table
* **Faster lookup:** One click shows everything in a room, without manual filtering
* **Improved user experience:** The floor plan is intuitive for users who are not familiar with reports or spreadsheets
* **Easier comparison:** Color-coded rooms and tooltips make it simple to compare how furniture is spread across the home
* **Reusable pattern:** The same approach can apply to other spatial data, such as office desks, warehouse zones or equipment by location

## 7. Skills Demonstrated

* Data visualization and dashboard design in Power BI
* Configuring and using a custom Power BI visual
* Mapping image regions to data fields for spatial reporting
* Setting up cross-filtering and interactions between visuals
* Aggregation and summary reporting (sum of quantity, totals)
* Translating a practical inventory need into a clear, user-friendly report

## 8. Future Enhancements

The following are **potential future enhancements**, not existing functionality:

* **Data quality checks:** Standardize category values (for example, the "Stoarge" entry should read "Storage") and align room names between the data and the floor plan labels
* **Richer attributes:** Add item value, condition, purchase date or photos to support insurance, moving or replacement planning
* **Pantry coverage:** Link the Pantry area, which currently shows no data, to inventory records
* **Live data source:** Connect to a maintained source such as SharePoint, Excel Online or a database with scheduled refresh
* **Additional views:** Add a bar chart of items by room or category, and slicers for furniture type
* **Publishing:** Publish to the Power BI Service for sharing on web and mobile

---

## Portfolio Summary

An interactive Power BI dashboard that maps a home's furniture inventory onto its floor plan. Each room is a clickable, color-coded region linked to an item table, so selecting a room filters the list and selecting an item highlights its room. Tooltips show item counts per room, and a total summarizes the full inventory of 38 items. The project demonstrates custom visual configuration, cross-filtering and location-based data storytelling.
