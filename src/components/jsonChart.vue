
<template>
<div class="container flex justify-center w-screen">
    <div class="">
      <h1 class="card-title text-[40px]">Direct VS Indirect</h1>
      <apexchart
        :type="chartType"
        width="800"
        :options="chartOptions"
        :series="series"
      ></apexchart>
    </div>
</div>
</template>

<script>
import VueApexCharts from "vue3-apexcharts";

export default {
  name:"json-chart",
  components: {
    apexchart: VueApexCharts,
  },
  props:{
      type:null,
      previousPeriodDatasets:null,
      currentPeriodDatasets:null,
      labels:null
  },
  
  data: function () {
    const _this = this;
    return {
      chartType: "bar",
      series: [
        {
            name: 'Previous Period',
            data: this.previousPeriodDatasets,
        },
        {
            name: 'Current Period',
            data: this.currentPeriodDatasets,
        },
    ],
    chartOptions: {
        colors: ['#5fa5fa', '#6266f1'],
        chart: {
            type: 'bar',

            toolbar: {
                show: false,
            },
        },
        dataLabels: {
            enabled: false,
        },
        stroke: {
            show: true,
            width: 2,
            colors: ['transparent'],
        },
        xaxis: {
            categories: this.labels,
            labels: { 
              formatter: function (value) {
                const months = ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"];
                const hours = ["AM", "PM"];
                const d = new Date(value);
                if(_this.type == "month") return months[d.getMonth()] + ' ' + d.getDay();
                else return d.getHours()%12 + ' ' + hours[Math.floor(d.getHours()/12)];
              }, 
            }
        },
        yaxis: {
          labels: {
            formatter: (val) => { 
              if(val >= 1000000) return '$'+val/1000000+'M';
              return '$' + val / 1000 + 'K'
            }
          }
        },
        fill: {
            opacity: 1,
        },
        legend:{
          position: 'top',
          markers: {
              width: 15,
              height: 15,
              strokeWidth: 15,
              strokeColor: 'black',
              fillColors: '#fff',
              radius: 20,
          },
          formatter: function(seriesName, opts) {
              var sum = 0;
              sum += parseInt(opts.w.globals.series[opts.seriesIndex]);
              var first="<b class='text-[20px]'>"+'$'+sum+"</b>";
              var second="<font class='text-[15px]'>"+seriesName+"</font>";
              return [first, second]
          }
        },
        tooltip: {
            y: {
                formatter: function (val) {
                    return '$ ' + val
                },
            },
        },
    },
    };
  },
};
</script>