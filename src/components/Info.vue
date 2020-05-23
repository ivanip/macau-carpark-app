<template>
    <f7-page @page:init="onPageInit">
        <f7-navbar :title="title" back-link="返回"></f7-navbar>
        <div class="info-container" v-if="typeof this.carpark !== 'undefined'">
            <div class="upper">
                <div class="numbers">
                    <div class="section">
                        <span>{{ this.carpark.car }}</span>
                        <h4>私家車位</h4>
                    </div>
                    <div class="section">
                        <span>{{ this.carpark.motor }}</span>
                        <h4>電單車位</h4>
                    </div>
                </div>
                <div class="address">
                    {{ this.carpark.address }}
                </div>
            </div>
            <div class="lower">
                <img :src="`https://maps.googleapis.com/maps/api/staticmap?center=${carpark.coordinates.lat},${carpark.coordinates.lng}&zoom=17&size=375x320&maptype=roadmap&markers=color:red|${carpark.coordinates.lat},${carpark.coordinates.lng}&key=AIzaSyDCxVlChY61Oohz7UooDcoc5YKxLwqaJHY`">
            </div>
        </div>
    </f7-page>
</template>

<script>
    export default {
        props: ['carpark'],
        data() {
            return {
                title: ''
            }
        },
        created() {
            if (typeof this.carpark === 'undefined') {
                this.$f7router.navigate('/', {reloadAll: true})
                return;
            }
        },
        methods: {
            onPageInit() {
                this.title = this.carpark.name
            }
        }
    }
</script>