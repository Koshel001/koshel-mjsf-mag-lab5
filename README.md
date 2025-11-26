# Vue Document Uploader

A modern, feature-rich Vue 3 component for file uploads with drag & drop support, file previews, and TypeScript support.

## Features

- 🎯 **Drag & Drop** - Intuitive drag and drop interface
- 📁 **Multiple File Upload** - Support for uploading multiple files
- 🖼️ **Image Previews** - Automatic preview generation for image files
- 📄 **Document Icons** - Display predefined document templates with custom icons
- 🎨 **Responsive Design** - Mobile-friendly grid layout
- 🔢 **File Limit Control** - Set maximum number of files
- ❌ **File Removal** - Easy removal of uploaded files
- 💪 **TypeScript Support** - Full TypeScript type definitions
- 🎨 **Customizable Styling** - Clean, modern design with scoped styles

## Installation

```bash
npm install @koshel/vue-document-uploader
```

or

```bash
yarn add @koshel/vue-document-uploader
```

## Usage

### Global Registration (as Plugin)

```typescript
import { createApp } from 'vue'
import App from './App.vue'
import DocumentUploaderPlugin from '@koshel/vue-document-uploader'
import '@koshel/vue-document-uploader/style.css'

const app = createApp(App)
app.use(DocumentUploaderPlugin)
app.mount('#app')
```

Then use it in your components:

```vue
<template>
  <DocumentUploader
    v-model="files"
    :documents="documents"
    :maxFiles="5"
  />
</template>

<script setup lang="ts">
import { ref } from 'vue'

const files = ref<File[]>([])
const documents = [
  { type: 'pdf', icon: '/icons/pdf.svg', name: 'Contract.pdf' },
  { type: 'docx', icon: '/icons/docx.svg', name: 'Report.docx' }
]
</script>
```

### Local Registration

```vue
<template>
  <DocumentUploader
    v-model="files"
    :documents="documents"
    :maxFiles="5"
  />
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { DocumentUploader } from '@koshel/vue-document-uploader'
import '@koshel/vue-document-uploader/style.css'

const files = ref<File[]>([])
const documents = [
  { type: 'pdf', icon: '/icons/pdf.svg', name: 'Contract.pdf' },
  { type: 'docx', icon: '/icons/docx.svg', name: 'Report.docx' }
]
</script>
```

## Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `modelValue` | `File[]` | `[]` | Array of uploaded files (v-model) |
| `documents` | `Document[]` | `[]` | Array of predefined documents to display |
| `maxFiles` | `number` | `10` | Maximum number of files allowed |

### Document Type

```typescript
interface Document {
  type: string    // File type (e.g., 'pdf', 'docx')
  icon: string    // Path to icon image
  name: string    // Display name of the document
}
```

## Events

| Event | Payload | Description |
|-------|---------|-------------|
| `update:modelValue` | `File[]` | Emitted when files are added or removed |

## Example with All Features

```vue
<template>
  <div class="app-container">
    <h1>Document Upload Demo</h1>

    <DocumentUploader
      v-model="uploadedFiles"
      :documents="availableDocuments"
      :maxFiles="5"
      @update:modelValue="handleFilesUpdate"
    />

    <div v-if="uploadedFiles.length > 0" class="file-list">
      <h2>Uploaded Files:</h2>
      <ul>
        <li v-for="(file, index) in uploadedFiles" :key="index">
          {{ file.name }} - {{ (file.size / 1024).toFixed(2) }} KB
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { DocumentUploader, type Document } from '@koshel/vue-document-uploader'
import '@koshel/vue-document-uploader/style.css'

const uploadedFiles = ref<File[]>([])

const availableDocuments: Document[] = [
  {
    type: 'pdf',
    icon: '/icons/pdf.svg',
    name: 'Contract.pdf'
  },
  {
    type: 'docx',
    icon: '/icons/docx.svg',
    name: 'Report.docx'
  },
  {
    type: 'xlsx',
    icon: '/icons/xlsx.svg',
    name: 'Data.xlsx'
  }
]

const handleFilesUpdate = (files: File[]) => {
  console.log('Files updated:', files)
  // Handle file upload logic here
}
</script>

<style scoped>
.app-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

.file-list {
  margin-top: 30px;
  padding: 20px;
  background: #f5f5f5;
  border-radius: 8px;
}
</style>
```

## Styling

The component comes with default styling, but you can customize it by overriding CSS variables or classes. The component uses scoped styles to avoid conflicts.

### Custom Styling Example

```css
/* Override default colors */
:root {
  --uploader-primary-color: #3b82f6;
  --uploader-border-color: #cbd5e1;
  --uploader-bg-color: #f8fafc;
}

/* Custom styles */
.document-uploader {
  /* Your custom styles */
}
```

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

## Development

### Setup

```bash
# Install dependencies
npm install

# Start development server
npm run dev

# Build library
npm run build:lib
```

### Building for Production

```bash
npm run build:lib
```

This will create optimized production builds in the `dist` directory.

## TypeScript

The package includes TypeScript declarations. If you're using TypeScript, you'll get full type safety and autocompletion.

```typescript
import type { Document, DocumentUploaderProps } from '@koshel/vue-document-uploader'
```

## License

MIT

