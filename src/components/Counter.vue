<template>
    <main class="countdown-wrapper" >
        <div class="counter" v-if="!expired">
            <div class="days-remaining">
                <p><span>{{displayDays}}</span> Days</p>
            </div>
            <div class="value-wrapper">
                <p>{{displayHours}}:{{displayMinutes}}:{{displaySeconds}}</p>
            </div>
        
        </div>
        <div class="expired" v-else>
            <p>EXPIRED</p>
        </div>
        <div class="date" v-if="finalDate">
            <p><i>until</i> {{ finalDate }}</p>
        </div>
    </main>
</template>

<script>
    export default {
        props: {
            year: Number,
            month: Number,
            date: Number,
            hour: Number,
            minute: Number,
            second: Number,
            ms: Number,
        },
        data: () => ({
            displayDays: 0,
            displayHours: 0,
            displayMinutes:0,
            displaySeconds:0,
            expired: false,
            timer: null,
            finalDate: null
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
            setRemaining() {
                const now = new Date();
                const distance = this.end.getTime() - now.getTime();

                if (distance < 0) {
                    if (this.timer !== null) {
                        clearInterval(this.timer); 
                    }
                    // countdown complete
                    this.expired = true;
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
            },
            showRemaining() {
                // sets on mount to show instantly
                this.setRemaining();
                
                // only starts the interval if the countdown has not expired
                if (this.expired) {
                    return;
                }

                // recaculates every second
                this.timer = setInterval(()=> {
                    this.setRemaining();
                }, 1000)
            },
            formatNum(num) {
                return num < 10 ? "0" + num : num;
            }
        },
        mounted() {
            this.showRemaining();
            const end = this.end;
            this.finalDate = end.toLocaleString("en-GB", {
                day: "numeric",
                month: "short",
                year: "numeric",
                hour: "numeric",
                minute: "2-digit"
            });

        }
    }
</script>

<style lang="scss" scoped>
p {
    font-size: 20px;
    color: white;
    letter-spacing: 1px;
    margin: 0 0 0.5rem 0;
}

.countdown-wrapper {
    display: flex;
    justify-content: center;
    text-align: center;
    flex-flow: column;
    background: rgb(63, 81, 181);
    width: 480px;
    margin: 16px auto;
    border-radius: 10px;
    padding: 35px 0 30px;
    box-sizing: border-box;
}

.countdown-wrapper > div {
    display: flex;
    flex-flow: row nowrap;
    justify-content: center;
    align-items: center;
}

.counter {
    gap: 10px;
}

.value-wrapper ,
.days-remaining,
.expired {
    p {
        font-size: 36px;
        font-weight: bold;
    }
}


</style>