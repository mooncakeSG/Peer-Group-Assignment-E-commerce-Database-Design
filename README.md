# Peer-Group-Assignment-E-commerce-Database-Design

# E-Commerce Database Project

## Project Overview
This repository contains a complete database design for an e-commerce platform. The project includes an Entity-Relationship Diagram (ERD), SQL schema creation scripts, and documentation for database structure and relationships.

## Group 339 

## Project Structure
- `/docs` - Contains documentation and the ERD diagram
- `/sql` - Contains SQL scripts for database creation and sample data
- `/examples` - Query examples demonstrating database functionality

## Database Design

### Entity-Relationship Diagram
The ERD visualizes the structure and relationships of our e-commerce database. It can be found in the `/docs` directory.

![E-Commerce Database ERD](docs/ecommerce_erd.png)

### Database Tables and Relationships

#### Core Product Information
- **brand**: Stores information about product manufacturers
  - Primary Key: `brand_id`
  - Relationships: One brand can have many products

- **product_category**: Classifies products into hierarchical categories
  - Primary Key: `category_id`
  - Self-referential relationship with `parent_category_id` for category hierarchy
  - Relationships: One category can contain many products

- **product**: Contains general product information
  - Primary Key: `product_id`
  - Foreign Keys: `brand_id`, `category_id`
  - Relationships: One product can have many product items, variations, attributes, and images

#### Product Variations
- **product_item**: Represents specific purchasable variations of products with inventory tracking
  - Primary Key: `item_id`
  - Foreign Key: `product_id`
  - Relationships: One product item can have many images

- **product_variation**: Links products to their variation options
  - Primary Key: `variation_id`
  - Foreign Keys: `product_id`, `size_option_id`, `color_id`

- **color**: Stores color options for products
  - Primary Key: `color_id`
  - Relationships: One color can be used in many product variations

- **size_category**: Categorizes types of sizes (clothing, shoes, etc.)
  - Primary Key: `size_category_id`
  - Relationships: One size category can have many size options

- **size_option**: Defines specific size values within a category
  - Primary Key: `size_option_id`
  - Foreign Key: `size_category_id`
  - Relationships: One size option can be used in many product variations

#### Product Attributes & Images
- **attribute_category**: Groups attributes into categories
  - Primary Key: `attribute_category_id`
  - Relationships: One attribute category can have many product attributes

- **attribute_type**: Defines data types for attributes
  - Primary Key: `attribute_type_id`
  - Relationships: One attribute type can be used by many product attributes

- **product_attribute**: Stores custom characteristics of products
  - Primary Key: `attribute_id`
  - Foreign Keys: `product_id`, `attribute_category_id`, `attribute_type_id`

- **product_image**: Stores image references for products
  - Primary Key: `image_id`
  - Foreign Keys: `product_id`, `product_item_id`
  - Relationships: Images can belong to general products or specific product items

### Database Schema

The complete SQL schema is available in the `/sql/ecommerce.sql` file. This script creates all tables with their respective columns, constraints, relationships, and indexes.

## Data Flow

1. **Product Creation Process**:
   - Create a brand (if new)
   - Select or create a product category
   - Create a product with general information
   - Define product attributes
   - Create variations (size/color combinations)
   - Add product items with specific SKUs and inventory
   - Upload product images

2. **Query Examples**:
   - Find all products from a specific brand
   - List products by category with their variations
   - Filter products by attributes
   - Get inventory levels for specific product items

## Implementation Notes

- **Indexing**: Foreign key columns are indexed to optimize query performance
- **Timestamps**: All tables include `created_at` and `updated_at` fields for auditing
- **Constraints**: Primary keys, foreign keys, and unique constraints maintain data integrity
- **Scalability**: The schema is designed to handle a wide variety of product types and attributes

## Setup Instructions

1. Clone this repository:
   ```
   git clone https://github.com/yourusername/ecommerce-database.git
   cd ecommerce-database
   ```

2. Create the database schema:
   ```
   mysql -u username -p your_database_name < sql/ecommerce.sql
   ```

3. Load sample data (optional):
   ```
   mysql -u username -p your_database_name < sql/sample_data.sql
   ```

4. Run example queries:
   ```
   mysql -u username -p your_database_name < examples/product_queries.sql
   ```

## Contribution Guidelines

1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Commit your changes: `git commit -m 'Add feature'`
4. Push to the branch: `git push origin feature-name`
5. Submit a pull request
