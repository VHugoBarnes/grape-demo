<script setup>
import { createApp, onMounted, h } from 'vue'
import Title from './components/Title.vue'
import Text from './components/Text.vue'
import ImageText from './components/ImageText.vue'

import grape from "grapesjs"
import 'grapesjs/dist/css/grapes.min.css'

let editor = null;

onMounted(() => {
  editor = grape.init({
    container: '#gjs',
    storageManager: {
      type: 'local' // Can be 'local', 'remote' or an object
    },
    canvas: {
      styles: [
        window.location.origin + '/css/style.css'
      ],
    },
    blockManager: {
      blocks: [
        {
          id: 'title-block',
          label: 'Titulo',
          content: '<div data-gjs-type="title-component"></div>',
          activate: true
        },
        {
          id: 'text-block',
          label: 'Texto',
          content: '<div data-gjs-type="text-component"></div>'
        },
        {
          id: 'image-text-block',
          label: 'Imagen y Texto',
          content: '<div data-gjs-type="image-text-component"></div>'
        }
      ]
    }
  });

  // Define custom components
  editor.DomComponents.addType('title-component', {
    isComponent: el => el.dataset.gjsType === 'title-component',
    model: {
      defaults: {
        tagName: 'h1',
        draggable: true,
        dropable: false,
        content: 'Título',
      }
    },
    view: {
      onRender() {
        const vueComponent = createApp({
          render: () => h(Title, {
            content: this.model.get('content'),
            onUpdateContent: content => {
              this.model.set({ content });
            },
          }),
        });
        this.el.innerHTML = '';
        vueComponent.mount(this.el)
      }
    }
  });

  editor.DomComponents.addType('text-component', {
    isComponent: el => el.tagName === 'DIV' && el.dataset.gjsType === 'text-component',
    model: {
      defaults: {
        tagName: 'p',
        draggable: true,
        droppable: false,
        components: [
          {
            type: 'text',
            tagName: 'p',
            content: 'Texto',
          },
        ],
      },
    },
    view: {
      onRender() {
        const vueComponent = createApp({
          render: () => h(Text, {
            props: {
              content: this.model.get('components').at(0).get('content'),
            },
            on: {
              'update:content': content => {
                this.model.get('components').at(0).set({ content });
              },
            },
          }),
        });
        vueComponent.mount(this.el)
      },
    },
  });

  editor.DomComponents.addType('image-text-component', {
    isComponent: el => el.tagName === 'DIV' && el.dataset.gjsType === 'image-text-component',
    model: {
      defaults: {
        tagName: 'div',
        draggable: true,
        droppable: false,
        components: [
          {
            type: 'image',
            tagName: 'img',
            src: 'https://via.placeholder.com/150',
            alt: 'Placeholder',
          },
          {
            type: 'text',
            tagName: 'p',
            content: 'Texto',
          },
        ],
      },
    },
    view: {
      onRender() {
        const vueComponent = createApp({
          render: () => h(ImageText, {
            props: {
              imageSrc: this.model.get('components').at(0).get('src'),
              imageAlt: this.model.get('components').at(0).get('alt'),
              content: this.model.get('components').at(1).get('content'),
            },
            on: {
              'update:content': content => {
                this.model.get('components').at(1).set({ content });
              },
            },
          }),
        });
        vueComponent.mount(this.el)
      },
    },
  });
});
</script>

<template>
  <div>
    <!-- Editor -->
    <div id="gjs"></div>
  </div>
</template>

<style scoped>
#gjs {
  height: 100vh !important;
  width: 100dvw !important;
}
</style>
