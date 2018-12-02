<template>
    <div>
        <input type="text" class="coupon-code" v-model="code" @input="validate">
        <p v-text="feedback"></p>
        <!--<p v-if="valid">-->
            <!--Coupon Redeemed: {{ message }}-->
        <!--</p>-->
        <!--<p v-else>-->
            <!--Invalid Coupon Code-->
        <!--</p>-->
    </div>
</template>

<script>
    export default {
        name: "CouponCode",

        data() {
            return {
                code: '',
                valid: false,
                coupons: [
                    {
                        code: '50OFF',
                        message: '50% OFF!',
                        discount: 50
                    },
                    {
                        code: 'FREE',
                        message: 'Entirely Free!',
                        discount: 100
                    }
                ]
            }
        },

        computed: {
            selectedCoupon() {
                return this.coupons.find(coupon => coupon.code == this.code);
            },
            message() {
                return this.selectedCoupon ? this.selectedCoupon.message : '';
            },
            feedback() {
                if (this.valid)
                    return `Coupon Redeemed: ${this.message}`;
                    // return 'Coupon Redeemed: ' + this.message;
                return 'Invalid Coupon Code';
            }
        },

        methods: {
            validate() {
                this.valid = !! this.selectedCoupon;
                // this.valid = this.coupons.map(coupon => coupon.code).includes(this.code);
                if (this.valid) {
                    this.$emit('applied', this.selectedCoupon.discount);
                }
            }
        }

    }
</script>
















