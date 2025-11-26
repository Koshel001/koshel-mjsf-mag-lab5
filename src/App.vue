<script setup lang="ts">
import { ref } from 'vue'
import DocumentUploader from './components/DocumentUploader.vue'

const uploadedFiles = ref<File[]>([])

const availableDocuments = [
  {
    type: 'pdf',
    icon: 'https://cdn-icons-png.flaticon.com/512/337/337946.png',
    name: 'Contract.pdf'
  },
  {
    type: 'docx',
    icon: 'https://cdn-icons-png.flaticon.com/512/281/281760.png',
    name: 'Report.docx'
  },
  {
    type: 'xlsx',
    icon: 'https://cdn-icons-png.flaticon.com/512/732/732220.png',
    name: 'Data.xlsx'
  }
]

const handleFilesUpdate = (files: File[]) => {
  console.log('Files updated:', files)
}
</script>

<template>
  <div class="app-container">
    <header class="app-header">
      <h1>📄 Vue Document Uploader</h1>
      <p class="subtitle">Drag & Drop File Upload Component</p>
    </header>

    <main class="app-main">
      <DocumentUploader
        v-model="uploadedFiles"
        :documents="availableDocuments"
        :maxFiles="5"
        @update:modelValue="handleFilesUpdate"
      />

      <div v-if="uploadedFiles.length > 0" class="file-list">
        <h2>Uploaded Files Summary:</h2>
        <ul>
          <li v-for="(file, index) in uploadedFiles" :key="index">
            <strong>{{ file.name }}</strong> - {{ (file.size / 1024).toFixed(2) }} KB
            <span class="file-type">({{ file.type || 'unknown' }})</span>
          </li>
        </ul>
        <p class="total-count">Total: {{ uploadedFiles.length }} file(s)</p>
      </div>
    </main>
  </div>
</template>

<style scoped>
.app-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
}

.app-header {
  text-align: center;
  margin-bottom: 40px;
}

.app-header h1 {
  font-size: 2.5rem;
  color: #1e293b;
  margin-bottom: 8px;
}

.subtitle {
  font-size: 1.2rem;
  color: #64748b;
  margin: 0;
}

.app-main {
  display: flex;
  flex-direction: column;
  gap: 30px;
}

.file-list {
  padding: 24px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border-radius: 12px;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
  color: white;
}

.file-list h2 {
  margin-top: 0;
  margin-bottom: 16px;
  font-size: 1.5rem;
}

.file-list ul {
  list-style: none;
  padding: 0;
  margin: 0 0 16px 0;
}

.file-list li {
  padding: 12px;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 6px;
  margin-bottom: 8px;
  backdrop-filter: blur(10px);
}

.file-type {
  color: rgba(255, 255, 255, 0.8);
  font-size: 0.9rem;
  margin-left: 8px;
}

.total-count {
  margin: 0;
  text-align: right;
  font-weight: 600;
  font-size: 1.1rem;
}

@media (max-width: 768px) {
  .app-header h1 {
    font-size: 2rem;
  }

  .subtitle {
    font-size: 1rem;
  }

  .app-container {
    padding: 16px;
  }
}
</style>
