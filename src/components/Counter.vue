<template>
    <main class="container" v-if="loaded">
        <div>
            <p>{{displayDays}}</p>
            <p>Days</p>
        </div>
        <div>
            <p>{{displayHours}}</p>
            <p>Hours</p>
        </div>
        <div>
            <p>{{displayMinutes}}</p>
            <p>Minutes</p>
        </div>
        <div>
            <p>{{displaySeconds}}</p>
            <p>Seconds</p>
        </div>
    </main>
</template>

<script>
    export default {
        props: ["year", "month", "date", "hour", "minute", "second", "ms"],
        data: () => ({
            displayDays: 0,
            displayHours: 0,
            displayMinutes:0,
            displaySeconds:0,
            loaded: false,
            expired: false,
        }),
        computed: {
            _seconds:() => 1000,
            _minutes() {
                return this._seconds * 60;
            },
            _hours() {
                return this._minutes * 60;
            },
            _days() {
                return this._hours * 24;
            },
            end() {
                return new Date(
                    this.year, 
                    this.month, 
                    this.date, 
                    this.hour, 
                    this.minute, 
                    this.second, 
                    this.ms
                    )
            }
        },
        methods: {
            showRemaining() {
                const timer = setInterval(()=> {
                    const now = new Date();
                    const distance = this.end.getTime() - now.getTime();

                    if (distance < 0) {
                        clearInterval(timer);
                        // countdown complete
                        this.expired = true;
                        this.loaded = true;
                        return;
                    }

                    const days = Math.floor((distance / this._days));
                    const hours = Math.floor((distance % this._days)/ this._hours);
                    const minutes = Math.floor((distance % this._hours)/ this._minutes);
                    const seconds = Math.floor((distance % this._minutes)/ this._seconds);

                    this.displayDays = this.formatNum(days);
                    this.displayHours = this.formatNum(hours);
                    this.displayMinutes = this.formatNum(minutes);
                    this.displaySeconds = this.formatNum(seconds);
                    this.loaded = true;

                }, 1000)
            },
            formatNum(num) {
                return num < 10 ? "0" + num : num;
            }
        },
        mounted() {
            this.showRemaining()
        }
    }
</script>

<style lang="scss" scoped>
p {
    font-family: Arial, Helvetica, sans-serif;
    font-size: 16px;
}

.container {
    display: flex;
    flex-flow: row nowrap;
    gap: 10px;
    justify-content: center;
    text-align: center;
}
</style>