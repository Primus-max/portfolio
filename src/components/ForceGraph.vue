<template>
  <svg :width="width" :height="height" class="force-graph">
    <g>
      <line v-for="(link, i) in validLinks" :key="'l'+i"
        v-if="link.source && link.target"
        :x1="getX(link.source)" :y1="getY(link.source)"
        :x2="getX(link.target)" :y2="getY(link.target)"
        stroke="#e3f0ff" stroke-width="2" />
      <g v-for="(node, i) in nodes" :key="'n'+i"
         v-if="node.x !== undefined && node.y !== undefined"
         class="node"
         :transform="`translate(${node.x},${node.y})`"
         @mousedown="startDrag(i, $event)"
         @mouseup="endDrag"
         @mouseleave="endDrag"
         @mousemove="drag($event)">
        <circle r="28" :fill="node.active ? '#3a7bd5' : '#fff'" stroke="#3a7bd5" stroke-width="3" />
        <text text-anchor="middle" dy=".35em" :fill="node.active ? '#fff' : '#3a7bd5'" font-size="13" font-weight="bold">
          <tspan v-for="(line, idx) in splitLabel(node.id)" :x="0" :dy="idx === 0 ? 0 : 15" :key="idx">{{ line }}</tspan>
        </text>
      </g>
    </g>
  </svg>
</template>

<script setup>
import {
  computed,
  onBeforeUnmount,
  onMounted,
  ref,
} from 'vue';

import {
  forceCenter,
  forceLink,
  forceManyBody,
  forceSimulation,
} from 'd3-force';

const width = 900
const height = 400

const nodes = ref([
  { id: 'C#' }, { id: '.NET' }, { id: 'ASP.NET Core' }, { id: 'Vue.js' },
  { id: 'JavaScript' }, { id: 'Docker' }, { id: 'CI/CD' }, { id: 'REST API' },
  { id: 'Entity Framework' }, { id: 'SQL' }, { id: 'SCSS' }, { id: 'Webpack' },
  { id: 'Git' }, { id: 'Playwright' }, { id: 'БЭМ' }
])
const links = ref([
  { source: 'C#', target: '.NET' },
  { source: '.NET', target: 'ASP.NET Core' },
  { source: 'Vue.js', target: 'JavaScript' },
  { source: 'Vue.js', target: 'SCSS' },
  { source: 'JavaScript', target: 'Webpack' },
  { source: 'Docker', target: 'CI/CD' },
  { source: 'Entity Framework', target: 'SQL' },
  { source: 'Git', target: 'CI/CD' },
  { source: 'Playwright', target: 'JavaScript' },
  { source: 'SCSS', target: 'БЭМ' }
])

const validLinks = computed(() =>
  links.value.filter(
    link =>
      link &&
      typeof link.source === 'object' &&
      typeof link.target === 'object'
  )
)

let simulation
let dragging = false
let dragNode = null

onMounted(() => {
  // Инициализация координат для всех узлов (по кругу)
  nodes.value.forEach((node, i) => {
    node.x = width / 2 + 120 * Math.cos((2 * Math.PI * i) / nodes.value.length);
    node.y = height / 2 + 120 * Math.sin((2 * Math.PI * i) / nodes.value.length);
  });
  simulation = forceSimulation(nodes.value)
    .force('link', forceLink(links.value).id(d => d.id).distance(130))
    .force('charge', forceManyBody().strength(-400))
    .force('center', forceCenter(width / 2, height / 2))
    .on('tick', () => {
      nodes.value.forEach(node => {
        node.x = Math.max(40, Math.min(width - 40, node.x));
        node.y = Math.max(40, Math.min(height - 40, node.y));
      });
    })
})

onBeforeUnmount(() => {
  simulation?.stop()
})

function startDrag(i, e) {
  dragging = true
  dragNode = nodes.value[i]
  dragNode.fx = dragNode.x
  dragNode.fy = dragNode.y
  dragNode.active = true
}
function drag(e) {
  if (!dragging || !dragNode) return
  const svgRect = e.target.ownerSVGElement.getBoundingClientRect()
  dragNode.fx = e.clientX - svgRect.left
  dragNode.fy = e.clientY - svgRect.top
}
function endDrag() {
  if (dragNode) dragNode.active = false
  dragging = false
  dragNode = null
}

// Функция для переноса длинных названий
function splitLabel(label) {
  if (label.length > 12) {
    const parts = label.split(' ')
    if (parts.length > 1) {
      return [parts.slice(0, -1).join(' '), parts[parts.length - 1]]
    } else {
      return [label.slice(0, 10) + '-', label.slice(10)]
    }
  }
  return [label]
}

function getX(node) {
  return node && typeof node === 'object' && node.x !== undefined ? node.x : 0;
}
function getY(node) {
  return node && typeof node === 'object' && node.y !== undefined ? node.y : 0;
}
</script>

<style scoped>
.force-graph {
  width: 100%;
  height: 400px;
  user-select: none;
  cursor: grab;
  background: #fff;
  border-radius: 1rem;
  box-shadow: 0 2px 8px #e3f0ff22;
}
.node text {
  pointer-events: none;
  font-family: 'Segoe UI', 'Roboto', 'Arial', sans-serif;
}
.node circle {
  transition: fill 0.2s;
}
</style> 