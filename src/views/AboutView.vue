<template>
    <div class="container-fluid">
        <div class="row">
            <div class="d-none d-md-block col-md-3">
                <img class="img-fluid" src="@/assets/bg.jpeg" alt="Background image" />
            </div>
            <div class="col-md-9 my-5">
                <form class="fw-bold text-uppercase mx-5">
                    <div class="row">
                        <div class="form-group col-md-6 mb-4 px-5">
                            <label for="first-name" class="form-label">
                                First name 
                                <span class="text-danger">*</span>
                            </label>
                            <input type="text" class="form-control" id="first-name">
                        </div>

                        <div class="form-group col-md-6 mb-4 px-5">
                            <label for="gender" class="form-label">
                                Gender 
                                <span class="text-danger">*</span>
                            </label>
                            <select class="form-select" id="gender">
                                <option selected disabled>Choose gender</option>
                                <option value="1">Male</option>
                                <option value="2">Female</option>
                            </select>
                        </div>

                        <div class="form-group col-md-6 mb-4 px-5">
                            <label for="last-name" class="form-label">
                                Last name 
                                <span class="text-danger">*</span>
                            </label>
                            <input type="text" class="form-control" id="last-name">
                        </div>

                        <div class="form-group col-md-6 mb-4 px-5">
                            <label class="form-label">
                                Payment mode 
                                <span class="text-danger">*</span>
                            </label>
                            <div class="text-capitalize fw-normal">
                                <div class="form-check form-check-inline">
                                    <input class="form-check-input" type="radio" name="inlineRadioOptions" id="inlineRadio1" value="Visa" checked>
                                    <label class="form-check-label" for="inlineRadio1">Visa</label>
                                </div>
                                <div class="form-check form-check-inline">
                                    <input class="form-check-input" type="radio" name="inlineRadioOptions" id="inlineRadio2" value="Mastercard">
                                    <label class="form-check-label" for="inlineRadio2">Mastercard</label>
                                </div>
                                <div class="form-check form-check-inline">
                                    <input class="form-check-input" type="radio" name="inlineRadioOptions" id="inlineRadio3" value="Amex">
                                    <label class="form-check-label" for="inlineRadio3">Amex</label>
                                </div>
                            </div>
                        </div>

                        <div class="form-group col-md-6 mb-4 px-5">
                            <label for="company" class="form-label">
                                Company 
                                <span class="text-danger">*</span>
                            </label>
                            <input type="text" class="form-control" id="company">
                        </div>

                        <div class="form-group col-md-6 mb-4 px-5">
                            <label for="card-number" class="form-label">
                                Card number 
                                <span class="text-danger">*</span>
                            </label>
                            <input type="text" class="form-control" id="card-number" placeholder="0000 0000 0000 0000" minlength="19" maxlength="19">
                        </div>

                        <div class="form-group col-md-6 mb-4 px-5">
                            <label for="email" class="form-label">
                                Email 
                                <span class="text-danger">*</span>
                            </label>
                            <input type="email" class="form-control" id="email">
                        </div>

                        <div class="form-group col-md-6 mb-4 px-5">
                            <label for="expiration" class="form-label">
                                Expiration 
                                <span class="text-danger">*</span>
                            </label>
                            <input type="month" class="form-control" id="expiration">
                        </div>

                        <div class="form-group col-md-6 mb-4 px-5">
                            <label for="phone" class="form-label">
                                Phone number 
                                <span class="text-danger">*</span>
                            </label>
                            <input type="tel" class="form-control" id="phone">
                        </div>

                        <div class="form-group col-md-6 mb-4 px-5">
                            <label for="cvn" class="form-label">
                                Cvn 
                                <span class="text-danger">*</span>
                            </label>
                            <input type="text" class="form-control" id="cvn" minlength="3" maxlength="3">
                        </div>

                        <div class="form-group mb-4 px-5 mt-4">
                            <label for="donate" class="form-label mb-4">
                                Donate us 
                                <span class="text-danger">*</span>
                            </label>
                            <div class="position-relative">
                                <input type="range" class="custom-range" id="donate" min="0" max="10000" step="10" v-model="donateValue" @input="updateValue()">
                                <!-- <span :style="styleSlider" ref="range-slider" class="range-slider">${{ donateValue }}</span> -->
                            </div>
                        </div>
                    </div>
                    <div class="text-end d-flex justify-content-md-end mt-4 px-5">
                        <button type="submit" class="btn btn-success px-2 me-md-2 text-uppercase">Submit</button>
                        <button type="reset" class="btn btn-outline-secondary px-2 text-uppercase">Reset</button>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                donateValue: 0,
                styleSlider: {
                    left: 0,
                    top: 0
                }
            }
        },
        methods: {
            updateValue() {
                const MAX_VALUE = 10000;
                console.log(this.donateValue);
                this.styleSlider.left = `${this.donateValue / MAX_VALUE * 100}%`;
            }
        }
    }
</script>

<style>
    .custom-range {
        -webkit-appearance: none;
        position: relative;
        width: 100%;
        height: 0.5rem;
        cursor: pointer;
        background: #f8f8f8;
    }
    .range-slider {
        position: absolute;
        background: #319e5e;
        color: #FFFFFF;
        display: inline-block;
        width: 5.2em;
        height: 2.2em;
        border-radius: 22px;
        line-height: 2.2em;
        text-align: center;
        z-index: 1;
        
    }
    .custom-range::-webkit-slider-thumb {
        -webkit-appearance: none;
        appearance: none;
        width: 25px;
        height: 25px;
        background: black;
        cursor: pointer;
        z-index: 10;
        position: relative;
    }

    .custom-range::after::-webkit-slider-thumb {
        position: absolute;
        left: 0;
        top: 0;
        content: "abc";
    }
</style>
