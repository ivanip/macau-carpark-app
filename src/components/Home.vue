<template>
    <f7-page ptr @ptr:refresh="refresh">
        <f7-navbar title="Macau Carpark Info"></f7-navbar>
        <f7-list>
            <f7-list-item class="item-link"
                          @click="$f7router.navigate('/info/', { props: {carpark: carpark} })"
                          :key="index"
                          :title="carpark.name"
                          :footer="`🚙 ${carpark.car} 🛵 ${carpark.motor}`"
                          v-for="(carpark, index) in carparkData">
                <f7-icon slot="media" icon="demo-list-icon"></f7-icon>
            </f7-list-item>
        </f7-list>
    </f7-page>
</template>

<script>
    export default {
        data() {
            return {
                carparkData: [],
            }
        },
        created() {
            fetch(`https://ios-dev.shortcutsapi.com/parking-info/parking-info-macau-ios-dev`)
                .then((res) => {
                    res.json().then((json) => {
                        // eslint-disable-next-line no-console
                        // console.log(json)
                        this.carparkData = json.data
                    })

                })
                .catch((err) => {
                    // eslint-disable-next-line no-console
                    console.log(err)
                })
        },
        methods: {
            refresh(done) {
                setTimeout(() => {
                    done()
                }, 1000)
            }
        }
    }
</script>
<style>
    .list .item-footer {
        color: #333;
        margin-top: .5em;
    }
</style>