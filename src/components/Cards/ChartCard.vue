<template>
  <div class="card">
    <div class="card-header" v-if="$slots.header">
      <slot name="header"></slot>
    </div>
    <div class="card-body">
      <div :id="chartId" class="ct-chart"></div>
    </div>
    <div class="card-footer" v-if="$slots.footer">
      <slot name="footer"></slot>
    </div>
  </div>
</template>
<script>
  import Card from './Card.vue'

  export default {
    name: 'chart-card',
    components: {
      Card
    },
    props: {
      chartType: {
        type: String,
        default: 'Line' // Line | Pie | Bar
      },
      chartOptions: {
        type: Object,
        default: () => {
          return {}
        }
      },
      chartData: {
        type: Object,
        default: () => {
          return {
            labels: [],
            series: []
          }
        }
      },
      responsiveOptions: [Object, Array]
    },
    data () {
      return {
        chartId: 'no-id',
        $Chartist: null,
        chart: null
      }
    },
    methods: {
      /***
       * Initializes the chart by merging the chart options sent via props and the default chart options
       */
      initChart () {
        var chartIdQuery = `#${this.chartId}`
        this.chart = this.$Chartist[this.chartType](chartIdQuery, this.chartData, this.chartOptions, this.responsiveOptions)
        this.$emit('initialized', this.chart)
        if (this.chartType === 'Line') {
  this.animateLineChart()
} else if (this.chartType === 'Bar') {
  this.animateBarChart()
} else if (this.chartType === 'Pie' && this.chartOptions.donut) {
  this.animateDonutChart()
}

      },
      /***
       * Assigns a random id to the chart
       */
      updateChartId () {
        const currentTime = new Date().getTime().toString()
        const randomInt = this.getRandomInt(0, currentTime)
        this.chartId = `div_${randomInt}`
      },
      getRandomInt (min, max) {
        return Math.floor(Math.random() * (max - min + 1)) + min
      },
      animateDonutChart() {
        const colors = ['#4285F4', '#EA4335', '#FBBC05', '#34A853', '#673AB7', '#FF6D00'];
      const chart = this.chart;
  
  chart.on('draw', (data) => {
    if (data.type === 'slice') {
      const pathLength = data.element._node.getTotalLength();
      
      data.element.attr({
        'stroke-dasharray': `${pathLength}px ${pathLength}px`,
        'stroke-dashoffset': `-${pathLength}px`,
        'stroke-linecap': 'butt',
        opacity: 1
      });

      data.element.animate({
        'stroke-dashoffset': {
          dur: 1000,
          from: `-${pathLength}px`,
          to: '0px',
          easing: this.$Chartist.Svg.Easing.easeOutQuint
        }
      });
    }
  });

  chart.on('created', () => {
    const chartSvg = document.querySelector(`#${this.chartId} svg`);
    if (!chartSvg) return;

    const tooltip = document.createElement('div');
    tooltip.className = 'chart-tooltip';
    chartSvg.parentNode.appendChild(tooltip);

    chartSvg.addEventListener('mousemove', (event) => {
      const paths = chartSvg.querySelectorAll('.ct-slice-donut');
      const mouseX = event.clientX;
      const mouseY = event.clientY;
      
      paths.forEach((path, index) => {
        if (this.isMouseOverPath(path, mouseX, mouseY)) {
          path.style.opacity = '0.7';
          path.style.transition = 'opacity 0.2s ease';
          
          // Enhanced tooltip with matching color
          tooltip.innerHTML = `
            <div class="tooltip-content" style="border-left: 4px solid ${colors[index]}">
              <strong>${this.chartData.labels[index]}</strong>
            </div>
          `;
          tooltip.style.display = 'block';
          tooltip.style.left = `${mouseX + 15}px`;
          tooltip.style.top = `${mouseY - 40}px`;
          tooltip.style.backgroundColor = `${this.hexToRgba(colors[index], 0.15)}`;
          tooltip.style.borderTop = `2px solid ${colors[index]}`;
        } else {
          path.style.opacity = '1';
        }
      });
    });

    chartSvg.addEventListener('mouseleave', () => {
      tooltip.style.display = 'none';
      const paths = chartSvg.querySelectorAll('.ct-slice-donut');
      paths.forEach(path => path.style.opacity = '1');
    });
  });
},

hexToRgba(hex, alpha) {
  const r = parseInt(hex.slice(1, 3), 16);
  const g = parseInt(hex.slice(3, 5), 16);
  const b = parseInt(hex.slice(5, 7), 16);
  return `rgba(${r}, ${g}, ${b}, ${alpha})`;
},

isMouseOverPath(path, mouseX, mouseY) {
  const rect = path.getBoundingClientRect();
  return mouseX >= rect.left && mouseX <= rect.right &&
         mouseY >= rect.top && mouseY <= rect.bottom;
},
      animateBarChart () {
        let seq = 0
        let durations = 500
        let delays = 80
        this.chart.on('draw', (data) => {
          if (data.type === 'bar') {
            seq++
            data.element.animate({
              opacity: {
                begin: seq * delays,
                dur: durations,
                from: 0,
                to: 1,
                easing: 'ease'
              }
            })
          }
        })
      }
    },
    async mounted () {
      this.updateChartId()
      const Chartist = await import('chartist')
      this.$Chartist = Chartist.default || Chartist
      this.initChart()
    }
  }
</script>
<style>

</style>
