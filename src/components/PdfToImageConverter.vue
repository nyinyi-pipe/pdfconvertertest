<!-- <template>
    <div>
      <input type="file" @change="handleFileChange" accept=".pdf" />
      <div v-if="imageData">
        <img :src="imageData" alt="Converted Image" />
      </div>
    </div>
  </template>
  
  <script>
  import { getDocument, GlobalWorkerOptions } from 'pdfjs-dist/build/pdf'
  
  export default {
    data() {
      return {
        imageData: null
      }
    },
    methods: {
      async handleFileChange(event) {
        const file = event.target.files[0]
  
        // Load the PDF file using pdf.js
        const loadingTask = getDocument(file)
        const pdf = await loadingTask.promise
  
        // Convert the first page of the PDF to an image
        const page = await pdf.getPage(1)
        const viewport = page.getViewport({ scale: 1.0 })
        const canvas = document.createElement('canvas')
        const context = canvas.getContext('2d')
        canvas.height = viewport.height
        canvas.width = viewport.width
  
        const renderTask = page.render({
          canvasContext: context,
          viewport: viewport
        })
  
        await renderTask.promise
  
        // Convert the canvas to base64 image data
        const imageDataURL = canvas.toDataURL()
  
        this.imageData = imageDataURL
      }
    },
    mounted() {
      GlobalWorkerOptions.workerSrc = require('pdfjs-dist/build/pdf.worker.entry')
    }
  }
  </script>
   -->


   <template>
    <div>
      <input type="file" @change="handleFileChange" accept=".pdf" />
      <div v-if="imageData">
        <img :src="imageData" alt="Converted Image" />
      </div>
    </div>
  </template>
  
  <script>
  import { getDocument, GlobalWorkerOptions } from 'pdfjs-dist/build/pdf'
  
  export default {
    data() {
      return {
        imageData: null
      }
    },
    methods: {
      async handleFileChange(event) {
        const file = event.target.files[0]
  
        // Create a file reader
        const reader = new FileReader()
  
        // Read the file as ArrayBuffer
        reader.readAsArrayBuffer(file)
  
        // Wait for the file to be loaded
        await new Promise(resolve => {
          reader.onload = resolve
        })
  
        // Get the array buffer of the file
        const arrayBuffer = reader.result
  
        // Load the PDF file using pdf.js
        const loadingTask = getDocument(arrayBuffer)
        const pdf = await loadingTask.promise
  
        // Convert the first page of the PDF to an image
        const page = await pdf.getPage(1)
        const viewport = page.getViewport({ scale: 1.0 })
        const canvas = document.createElement('canvas')
        const context = canvas.getContext('2d')
        canvas.height = viewport.height
        canvas.width = viewport.width
  
        const renderTask = page.render({
          canvasContext: context,
          viewport: viewport
        })
  
        await renderTask.promise
  
        // Convert the canvas to base64 image data
        const imageDataURL = canvas.toDataURL()
  
        this.imageData = imageDataURL
      }
    },
    mounted() {
      GlobalWorkerOptions.workerSrc = require('pdfjs-dist/build/pdf.worker.entry')
    }
  }
  </script>
  