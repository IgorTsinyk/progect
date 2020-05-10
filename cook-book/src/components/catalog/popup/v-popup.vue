<template>
    <div class="popup">
        <div class="v-popup-heder">
            <span>Name</span>
            <span>
                <i 
                class="material-icons"
                @click="closePopup"
                >
                close
                </i>
            </span>
        </div>
        <div class="v-popup-content">
            <slot></slot>
        </div>
        <div class="v-popup-footer">
            <button 
            class="close-btn"
            @click="closePopup"
            >
            Close
            </button>
            <button 
            class="submit-btn"
            @click="rightBtnAction"
            >
            {{rightBtnTitle}}
            </button>
        </div>
    </div>
</template>

<script>
    export default {
        name: "popup",
        data(){
            return{}
        },
        computed: {},
        methods: {
            closePopup(){
                this.$emit('closePopup')
            },
            rightBtnAction(){
                this.$emit ('rightBtnAction')
            }
        },
        props:{
            rightBtnTitle:{
                type: String,
                default: 'Ok'
            }
        }
        
    }
</script>

<style>
.v-popup{
    padding: 16px;
    position: fixed;
    top: 50px;
    width: 400px;
    background: #ffffff;
    box-shadow: 0 0 17px 0 #e7e7e7;
}
.v-popup-heder, .v-popup-footer{
    padding: 16px;
    position: fixed;
    top: 50px;
    width: 400px;
    background: #ffffff;
    box-shadow: 0 0 17px 0 #e7e7e7;
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.v-popup-content{
    padding: 16px;
    position: fixed;
    top: 50px;
    width: 400px;
    background: #ffffff;
    box-shadow: 0 0 17px 0 #e7e7e7;
    display: flex;
    justify-content: center;
    align-items: center;
}
.submit-btn{
    padding: 8px;
    background: gray;
}

</style>