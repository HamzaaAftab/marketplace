Day 3

## Overview
This documentation provides an overview of the work completed during **Day 3** of the Marketplace Builder Hackathon 2025. The day focused on:
- **API Integration**
- **Data Migration**
- **Error Handling**
- **Asynchronous Operations**

### Key Accomplishments
- Successfully integrated APIs into the marketplace application.
- Migrated and optimized data to improve performance and scalability.
- Handled edge cases for efficient and smooth data flows.
- Enhanced application performance through improved asynchronous operations.

---

## Sanity Schema for Product
Here is the schema definition for the `Product` document in **Sanity Studio**:

```typescript
import { ShoppingBagIcon } from "lucide-react";
import { defineType } from "sanity";

export const product = defineType({
    name: "product",
    title: "Product",
    type: "document",
    icon: ShoppingBagIcon,
    fields: [
        {
            name: "title",
            title: "Title",
            validation: (rule) => rule.required(),
            type: "string"
        },
        {
            name: "description",
            type: "text",
            validation: (rule) => rule.required(),
            title: "Description",
        },
        {
            name: "productImage",
            type: "image",
            validation: (rule) => rule.required(),
            title: "Product Image"
        },
        {
            name: "price",
            type: "number",
            validation: (rule) => rule.required(),
            title: "Price",
        },
        {
            name: "tags",
            type: "array",
            title: "Tags",
            of: [{ type: "string" }]
        },
        {
            name: "dicountPercentage",
            type: "number",
            title: "Discount Percentage",
        },
        {
            name: "isNew",
            type: "boolean",
            title: "New Badge",
        }
    ]
});
```

---

## API Fetching Code Snippet
This is the API fetching code to retrieve the `Product` data from Sanity:

```javascript
const res = await client.fetch(groq`*[_type=="product"]{
    _id,
    title,
    "imageUrl": productImage.asset->url,
    price,
    tags,
    dicountPercentage,
    description,
    isNew
}`);
```

---

## Importing Data to Sanity
Here is the code snippet to upload product images and data to Sanity:

```javascript
import { createClient } from '@sanity/client';

const client = createClient({
    projectId: '63kj3oiu',
    dataset: 'production',
    useCdn: true,
    apiVersion: '2025-01-13',
    token: '<your-token>'
});

async function uploadImageToSanity(imageUrl) {
    try {
        console.log(`Uploading image: ${imageUrl}`);
        const response = await fetch(imageUrl);
        if (!response.ok) {
            throw new Error(`Failed to fetch image: ${imageUrl}`);
        }

        const buffer = await response.arrayBuffer();
        const bufferImage = Buffer.from(buffer);

        const asset = await client.assets.upload('image', bufferImage, {
            filename: imageUrl.split('/').pop(),
        });

        console.log(`Image uploaded successfully: ${asset._id}`);
        return asset._id;
    } catch (error) {
        console.error(`Failed to upload image:`, imageUrl, error);
        return null;
    }
}
```

---

## Key Learnings
1. **Error Handling:** Importance of robust error handling mechanisms in API calls.
2. **Data Migration:** Strategies to build efficient and maintainable migration scripts.
3. **Asynchronous Operations:** Techniques to improve efficiency and reduce bottlenecks.
4. **Teamwork:** Collaboration and persistence are essential for overcoming challenges.

---

## Next Steps
1. **Refining UI**: Further enhance the application's user interface and experience.
2. **Implement Shipment and Payment Methods**: Add functionalities for order shipment tracking and integration of payment gateways.
3. **Deployment**: Prepare the application for deployment.
4. **Team Collaboration**: Collaborate with teammates to finalize features and ensure alignment across all modules.

---

## Acknowledgments
Special thanks to **Sir Ali Jawwad** and **Sir Ameen Alam** for their mentorship and guidance throughout this hackathon. Their support has been invaluable in achieving these milestones.

