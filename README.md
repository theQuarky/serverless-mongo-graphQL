# Serverless MongoDB GraphQL

A full-stack serverless application built with GraphQL, MongoDB, and React. This project demonstrates a modern serverless architecture with a GraphQL API backend deployed on AWS Lambda and a React TypeScript frontend.

## 🏗️ Architecture

The project consists of two main parts:

- **Backend**: Serverless GraphQL API using Apollo Server Lambda, connected to MongoDB Atlas
- **Frontend**: React TypeScript application with Apollo Client for GraphQL queries and mutations

## ✨ Features

- **CRUD Operations**: Create, Read, Update, and Delete attributes
- **GraphQL API**: Type-safe API with GraphQL schema
- **Serverless Deployment**: AWS Lambda functions with Serverless Framework
- **MongoDB Integration**: Cloud-based MongoDB Atlas database
- **React Frontend**: Modern React with TypeScript and Apollo Client
- **Type Safety**: TypeScript for frontend and GraphQL code generation
- **Offline Development**: Local development support with serverless-offline

## 🛠️ Tech Stack

### Backend
- [Node.js](https://nodejs.org/) - JavaScript runtime
- [Apollo Server Lambda](https://www.apollographql.com/docs/apollo-server/) - GraphQL server for AWS Lambda
- [GraphQL](https://graphql.org/) - API query language
- [MongoDB](https://www.mongodb.com/) with [Mongoose](https://mongoosejs.com/) - Database and ODM
- [Serverless Framework](https://www.serverless.com/) - AWS Lambda deployment
- [serverless-offline](https://github.com/dherault/serverless-offline) - Local development

### Frontend
- [React](https://reactjs.org/) - UI library
- [TypeScript](https://www.typescriptlang.org/) - Type-safe JavaScript
- [Apollo Client](https://www.apollographql.com/docs/react/) - GraphQL client
- [GraphQL Code Generator](https://www.graphql-code-generator.com/) - Type generation

## 📋 Prerequisites

Before you begin, ensure you have the following installed:

- [Node.js](https://nodejs.org/) (v14 or higher)
- [npm](https://www.npmjs.com/) or [yarn](https://yarnpkg.com/)
- [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) account (or local MongoDB instance)
- [AWS Account](https://aws.amazon.com/) (for deployment)
- [Serverless Framework](https://www.serverless.com/) CLI (install with `npm install -g serverless`)

## 🚀 Getting Started

### Backend Setup

1. **Navigate to the backend directory**:
   ```bash
   cd backend
   ```

2. **Install dependencies**:
   ```bash
   npm install
   # or
   yarn install
   ```

3. **Configure MongoDB connection**:
   - Open `backend/db.js`
   - Replace the MongoDB connection string with your own:
   ```javascript
   await mongoose.connect(
       "your-mongodb-connection-string",
       { useNewUrlParser: true }
   );
   ```

4. **Start the local development server**:
   ```bash
   npm start
   # or
   yarn start
   ```
   
   The GraphQL endpoint will be available at `http://localhost:4000/graphql`

### Frontend Setup

1. **Navigate to the frontend directory**:
   ```bash
   cd frontend
   ```

2. **Install dependencies**:
   ```bash
   npm install
   # or
   yarn install
   ```

3. **Configure GraphQL endpoint** (if needed):
   - Create a `.env` file in the frontend directory
   - Add your GraphQL endpoint:
   ```
   REACT_APP_GRAPHQL_ENDPOINT=http://localhost:4000/graphql
   ```

4. **Start the development server**:
   ```bash
   npm start
   # or
   yarn start
   ```
   
   The application will open at `http://localhost:3000`

## 📖 GraphQL Schema

### Types

```graphql
type AttributeType {
  id: String!
  name: String!
  type: String!
  placeholder: String
  options: [String!]
}
```

### Queries

```graphql
# Get all attributes
attributes: [AttributeType]

# Get a single attribute by ID
attribute(id: String!): AttributeType
```

### Mutations

```graphql
# Add a new attribute
addAttribite(input: AttributeAddInput): AttributeType

# Update an existing attribute
updateAttribute(input: AttributeUpdateInput!): AttributeType

# Delete an attribute
deleteAttribute(id: String!): AttributeType
```

## 🎯 Usage Examples

### Query All Attributes

```graphql
query GetAttributes {
  attributes {
    id
    name
    type
    placeholder
    options
  }
}
```

### Add an Attribute

```graphql
mutation AddAttribute($input: AttributeAddInput) {
  addAttribite(input: $input) {
    id
    name
    type
    placeholder
    options
  }
}
```

Variables:
```json
{
  "input": {
    "name": "Email",
    "type": "T",
    "placeholder": "Enter your email"
  }
}
```

### Update an Attribute

```graphql
mutation UpdateAttribute($input: AttributeUpdateInput!) {
  updateAttribute(input: $input) {
    id
    name
    type
    placeholder
    options
  }
}
```

### Delete an Attribute

```graphql
mutation DeleteAttribute($id: String!) {
  deleteAttribute(id: $id) {
    id
    name
  }
}
```

## 🚢 Deployment

### Backend Deployment to AWS Lambda

1. **Configure AWS credentials**:
   ```bash
   serverless config credentials --provider aws --key YOUR_ACCESS_KEY --secret YOUR_SECRET_KEY
   ```

2. **Deploy to AWS**:
   ```bash
   cd backend
   serverless deploy
   ```

3. **Note the deployed endpoint URL** and update the frontend environment variable

### Frontend Deployment

The frontend can be deployed to various hosting platforms:

- **Vercel**: `vercel deploy`
- **Netlify**: Connect your GitHub repository
- **AWS S3 + CloudFront**: 
  ```bash
  npm run build
  aws s3 sync build/ s3://your-bucket-name
  ```

## 📁 Project Structure

```
serverless-mongo-graphQL/
├── backend/
│   ├── attribute/
│   │   ├── schema.js       # GraphQL type definitions
│   │   ├── resolvers.js    # GraphQL resolvers
│   │   ├── model.js        # Mongoose model
│   │   └── db.js           # Database helper functions
│   ├── handler.js          # Lambda handler
│   ├── db.js               # Database connection
│   ├── serverless.yml      # Serverless configuration
│   └── package.json
├── frontend/
│   ├── src/
│   │   ├── App.tsx         # Main React component
│   │   └── index.tsx       # React entry point
│   ├── public/
│   ├── codegen.ts          # GraphQL code generation config
│   └── package.json
└── README.md
```

## 🔧 Available Scripts

### Backend

- `npm start` - Start local development server with serverless-offline
- `npm run devStart` - Start with nodemon for auto-reload
- `serverless deploy` - Deploy to AWS Lambda
- `serverless remove` - Remove deployment from AWS

### Frontend

- `npm start` - Start development server (runs on port 3000)
- `npm run build` - Build production-ready application
- `npm test` - Run tests
- `npm run codegen` - Generate TypeScript types from GraphQL schema

## 🔐 Environment Variables

### Backend

The backend uses hardcoded MongoDB connection string in `db.js`. For production, use environment variables:

```bash
# In serverless.yml
provider:
  environment:
    MONGODB_URI: ${env:MONGODB_URI}
```

### Frontend

Create a `.env` file:

```env
REACT_APP_GRAPHQL_ENDPOINT=your-graphql-endpoint
```

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is open source and available under the [ISC License](LICENSE).

## 👤 Author

Created by [theQuarky](https://github.com/theQuarky)

## 🐛 Known Issues

- The mutation name has a typo: `addAttribite` should be `addAttribute`
- MongoDB credentials are hardcoded in the source code (should use environment variables)
- Some error handling can be improved

## 🔮 Future Improvements

- [ ] Add authentication and authorization
- [ ] Implement input validation on backend
- [ ] Add comprehensive error handling
- [ ] Add unit and integration tests
- [ ] Implement pagination for attributes list
- [ ] Add search and filter functionality
- [ ] Improve UI/UX design
- [ ] Add Docker support for local development
- [ ] Implement CI/CD pipeline
- [ ] Add API rate limiting
- [ ] Use environment variables for configuration

## 📚 Additional Resources

- [Serverless Framework Documentation](https://www.serverless.com/framework/docs/)
- [Apollo Server Documentation](https://www.apollographql.com/docs/apollo-server/)
- [GraphQL Documentation](https://graphql.org/learn/)
- [React Documentation](https://reactjs.org/docs/getting-started.html)
- [MongoDB Atlas Documentation](https://docs.atlas.mongodb.com/)

## 💬 Support

For issues and questions, please open an issue on GitHub or contact the repository maintainer.

---

Made with ❤️ using Serverless, GraphQL, MongoDB, and React
