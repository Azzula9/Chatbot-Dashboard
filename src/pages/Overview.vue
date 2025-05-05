<template>
  <div class="content">
    <div class="cohntainer-fluid">
      <div class="mb-3 px-3">
        <p class="h5 text-dark">
          🐝 Back in the hive, Jane! Let’s make this chatbot bee-yond awesome
        </p>
      </div>
      <card class="stats-wrapper-card">
  <div class="d-flex justify-content-between align-items-center px-3 pt-3 pb-1">
    <h4 class="card-title mb-0 " style="font-weight: bold;"> Statistics</h4>
    <p class="card-category mb-0 text-muted small">
      This report was generated on 15/04/2025 at 1:50:09 PM - 
      <a href="#" class="text-success">Refresh</a>
    </p>
  </div>

  <div class="row p-3">
    <div class="col-xl-3 col-md-6">
      <stats-card>
        <div slot="header" class="icon-warning">
          <i class="pi pi-envelope text-warning"></i>
        </div>
        <div slot="content" class="stats-card-padding">
          <p class="card-category">Chat Sessions</p>
          <h4 class="card-title">5,905</h4>
        </div>
      </stats-card>
    </div>

    <div class="col-xl-3 col-md-6">
      <stats-card>
        <div slot="header" class="icon-success">
          <i class="pi pi-paperclip text-success"></i>
        </div>
        <div slot="content" class="stats-card-padding">
          <p class="card-category">Bot Accuracy</p>
          <h4 class="card-title">%95</h4>
        </div>
      </stats-card>
    </div>

    <div class="col-xl-3 col-md-6">
      <stats-card>
        <div slot="header" class="icon-danger">
          <i class="pi pi-clock text-danger"></i>
        </div>
        <div slot="content" class="stats-card-padding">
          <p class="card-category">Avg.Response Time</p>
          <h4 class="card-title">2.4s</h4>
        </div>
      </stats-card>
    </div>
<!-- *start* -->
    <div class="col-xl-3 col-md-6">
      <stats-card>
        <div slot="header" class="icon-info">
          <i class="pi pi-chart-line text-primary"></i>
        </div>
        <div slot="content" class="stats-card-padding">
          <p class="card-category">Escalation Rate</p>
          <h4 class="card-title">%17</h4>
        </div>
      </stats-card>
    </div>
  </div>
</card>
      </div>
      <div class="row">
        <div class="col-md-8">
          <chart-card :chart-data="lineChart.data"
                      :chart-options="lineChart.options"
                      :responsive-options="lineChart.responsiveOptions">
            <template slot="header">
              <h4 class="card-title">Users Behavior</h4>
              <p class="card-category">24 Hours performance</p>
            </template>
            <template slot="footer">
              <div class="legend">
                <i class="fa fa-circle text-info"></i> Open
                <i class="fa fa-circle text-danger"></i> Click
                <i class="fa fa-circle text-warning"></i> Click Second Time
              </div>
              <hr>
              <div class="stats">
                <i class="fa fa-history"></i> Updated 3 minutes ago
              </div>
            </template>
          </chart-card>
        </div>

        <div class="col-md-4">
          <chart-card :chart-data="pieChart.data" :chart-options="pieChart.options" chart-type="Pie">
            <template slot="header">
              <h4 class="card-title">Most Common Chat Topics</h4>
              <p class="card-category text-primary">See full report</p>
            </template>
            <template slot="footer">
              <div class="legend" style="display: flex; flex-wrap: wrap; gap: 16px; margin-top: 20px;">
  <div style="display: flex; align-items: center;">
    <span style="width: 12px; height: 12px; background-color: #FF6B6B; border-radius: 50%; display: inline-block; margin-right: 6px;"></span>
    Order Status
  </div>
  <div style="display: flex; align-items: center;">
    <span style="width: 12px; height: 12px; background-color: #FFA94D; border-radius: 50%; display: inline-block; margin-right: 6px;"></span>
    New Orders
  </div>
  <div style="display: flex; align-items: center;">
    <span style="width: 12px; height: 12px; background-color: #FFD43B; border-radius: 50%; display: inline-block; margin-right: 6px;"></span>
    Payment Issues
  </div>
  <div style="display: flex; align-items: center;">
    <span style="width: 12px; height: 12px; background-color: #4DABF7; border-radius: 50%; display: inline-block; margin-right: 6px;"></span>
    Missing/Wrong Items
  </div>
  <div style="display: flex; align-items: center;">
    <span style="width: 12px; height: 12px; background-color: #69DB7C; border-radius: 50%; display: inline-block; margin-right: 6px;"></span>
    Promos & Discounts
  </div>
  <div style="display: flex; align-items: center;">
    <span style="width: 12px; height: 12px; background-color: #D0BFFF; border-radius: 50%; display: inline-block; margin-right: 6px;"></span>
    Receipts & History
  </div>
</div>

              <!-- <hr> -->
            
            </template>
          </chart-card>
        </div>
      </div>
<!-- end -->
      <div class="row">
        <div class="col-md-6">
          <chart-card
            :chart-data="barChart.data"
            :chart-options="barChart.options"
            :chart-responsive-options="barChart.responsiveOptions"
            chart-type="Bar">
            <template slot="header">
              <h4 class="card-title">2014 Sales</h4>
              <p class="card-category">All products including Taxes</p>
            </template>
            <template slot="footer">
              <div class="legend">
                <i class="fa fa-circle text-info"></i> Tesla Model S
                <i class="fa fa-circle text-danger"></i> BMW 5 Series
              </div>
              <hr>
              <div class="stats">
                <i class="fa fa-check"></i> Data information certified
              </div>
            </template>
          </chart-card>
        </div>

        <div class="col-md-6">
          <card>
            <template slot="header">
              <h5 class="title">Tasks</h5>
              <p class="category">Backend development</p>
            </template>
            <l-table :data="tableData.data"
                     :columns="tableData.columns">
              <template slot="columns"></template>

              <template slot-scope="{row}">
                <td>
                  <base-checkbox v-model="row.checked"></base-checkbox>
                </td>
                <td>{{row.title}}</td>
                <td class="td-actions text-right">
                  <button type="button" class="btn-simple btn btn-xs btn-info" v-tooltip.top-center="editTooltip">
                    <i class="fa fa-edit"></i>
                  </button>
                  <button type="button" class="btn-simple btn btn-xs btn-danger" v-tooltip.top-center="deleteTooltip">
                    <i class="fa fa-times"></i>
                  </button>
                </td>
              </template>
            </l-table>
            <div class="footer">
              <hr>
              <div class="stats">
                <i class="fa fa-history"></i> Updated 3 minutes ago
              </div>
            </div>
          </card>

        </div>
      </div>
    </div>
</template>
<script>
  import ChartCard from 'src/components/Cards/ChartCard.vue'
  import StatsCard from 'src/components/Cards/StatsCard.vue'
  import LTable from 'src/components/Table.vue'

  export default {
    components: {
      LTable,
      ChartCard,
      StatsCard
    },
    data () {
      return {
        editTooltip: 'Edit Task',
        deleteTooltip: 'Remove',
        // strat
        pieChart: {
  data: {
    labels: ['35%', '15%', '10%', '10%', '5%', '25%'],
    series: [35, 15, 10, 10, 5, 25]
  },
  options: {
    donut: true,
    donutWidth: 50,
    showLabel: false,
    startAngle: 270,
    chartPadding: 20,
    stroke: {
      lineCap: 'butt', // Creates square edges
  }
},

plugins: [
      {
        beforeDraw: function(chart) {
          if (chart.options.donut) {
            // Add gaps between segments (3px)
            const gapSize = 2;
            const seriesTotal = chart.data.series.reduce((a, b) => a + b, 0);
            
            chart.svg.querySelectorAll('.ct-slice-donut').forEach((slice, i) => {
              const pathLength = slice.getTotalLength();
              const segmentRatio = chart.data.series[i] / seriesTotal;
              const gapRatio = gapSize / (chart.options.donutWidth * Math.PI);
              const visibleLength = pathLength * (1 - gapRatio / segmentRatio);
              
              slice.style.strokeDasharray = `${visibleLength} ${pathLength - visibleLength}`;
              slice.style.strokeDashoffset = -pathLength;
            });
          }
        }
      },
      {
        beforeDraw: function(chart) {
          if (chart.options.plugins.ctCenterText) {
            const centerText = chart.options.plugins.ctCenterText;
            const width = chart.width;
            const height = chart.height;
            
            chart.svg.elem('text', {
              x: width / 4,
              y: height / 4,
              'text-anchor': 'middle',
              'dominant-baseline': 'middle',
              style: `font-size: ${centerText.size || '16px'}; font-weight: ${centerText.weight || 'bold'}`
            }, 'ct-center-text', true).text(centerText.text || '');
          }
        }
      }
    ],
        },
        lineChart: {
          data: {
            labels: ['9:00AM', '12:00AM', '3:00PM', '6:00PM', '9:00PM', '12:00PM', '3:00AM', '6:00AM'],
            series: [
              [287, 385, 490, 492, 554, 586, 698, 695],
              [67, 152, 143, 240, 287, 335, 435, 437],
              [23, 113, 67, 108, 190, 239, 307, 308]
            ]
          },
          options: {
            low: 0,
            high: 800,
            showArea: false,
            height: '245px',
            axisX: {
              showGrid: false
            },
            lineSmooth: true,
            showLine: true,
            showPoint: true,
            fullWidth: true,
            chartPadding: {
              right: 50
            }
          },
          responsiveOptions: [
            ['screen and (max-width: 640px)', {
              axisX: {
                labelInterpolationFnc (value) {
                  return value[0]
                }
              }
            }]
          ]
        },
        // end
        barChart: {
          data: {
            labels: ['Jan', 'Feb', 'Mar', 'Apr', 'Mai', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
            series: [
              [542, 443, 320, 780, 553, 453, 326, 434, 568, 610, 756, 895],
              [412, 243, 280, 580, 453, 353, 300, 364, 368, 410, 636, 695]
            ]
          },
          options: {
            seriesBarDistance: 10,
            axisX: {
              showGrid: false
            },
            height: '245px'
          },
          responsiveOptions: [
            ['screen and (max-width: 640px)', {
              seriesBarDistance: 5,
              axisX: {
                labelInterpolationFnc (value) {
                  return value[0]
                }
              }
            }]
          ]
        },
        tableData: {
          data: [
            {title: 'Sign contract for "What are conference organizers afraid of?"', checked: false},
            {title: 'Lines From Great Russian Literature? Or E-mails From My Boss?', checked: true},
            {
              title: 'Flooded: One year later, assessing what was lost and what was found when a ravaging rain swept through metro Detroit',
              checked: true
            },
            {title: 'Create 4 Invisible User Experiences you Never Knew About', checked: false},
            {title: 'Read "Following makes Medium better"', checked: false},
            {title: 'Unfollow 5 enemies from twitter', checked: false}
          ]
        }
      }
    }
  }
</script>
<style>

</style>
