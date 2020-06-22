<template>
<v-container>

    <h1>Chart</h1>
    <v-row>
        <v-col :cols="4">
            <v-date-picker v-model="date" @change="dateChange" ></v-date-picker>
        </v-col>
        <v-col :cols="8">
            <line-chart v-if="!loading" :chartdata="chartData" :options="chartOptions"/>
        </v-col>
    </v-row>
</v-container>

</template>

<script>
import LineChart from '../components/charts/LineChart';
import moment from 'moment';

export default {
    components: {
        'line-chart': LineChart
    },
    middleware: 'auth',
    data() {
        return {
            date: new Date().toISOString().substr(0, 10),
            loading: true,
            chartData: {
                labels: ['January', 'February'],
                datasets: [
                    {
                        label: 'User registration',
                        backgroundColor: '#f87979',
                        data: [40, 20]
                    }
                ]
            },
            chartOptions: {
                responsive: true,
                maintainAspectRatio: false
            }
        };
    },
    mounted() {
        this.getChartData();
    },
    methods: {
        async getChartData() {
            this.loading = true;
            let {date} = this;
            
            let data = await this.$axios.get('/user/get-users', {params:{date}});
            this.chartData.labels = data.data.data.map(item => {
                let d = new Date(item.createdAt);

                return moment(d).format('MM/DD hh:mm');
            });
            this.chartData.datasets[0].data = data.data.data.map(item => {
                let d = item.createdAt
                return new Date(item.createdAt).getHours();
            });
            
            this.loading = false;
        },
        dateChange() {
            this.getChartData();
        }
    }
}
</script>