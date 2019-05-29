<template>
    <ion-grid>
        <form @submit="onSubmit">
            <ion-col>
                <ion-item>
                    <ion-label>ZipCode: </ion-label>
                    <ion-input placeholder="Enter a US ZipCode" :value="zip" @input="zip = $event.target.value" name="zip"></ion-input>
                </ion-item>  
            </ion-col>
            <ion-col>
                <ion-button type="submit" color="primary" expand="block">Find</ion-button>
            </ion-col>
        </form>
    </ion-grid>
</template>

<script>
export default {
    name: "ZipSearch",
    data() {
        return {
            "zip": "" 
        }
    }, 
    methods: {
        onSubmit(e) {
            e.preventDefault()
            
            // ZIP Regex
            const isValidZip = /(^\d{5}$)|(^\d{5}-\d{4}$)/.test(this.zip)

            // Test for valid ZIP
            if (!isValidZip) {
                this.showAlert()
                this.zip = ""
            } else {
                this.$emit("get-zip", this.zip)
                this.zip = ""
            }
        },
        showAlert() {
            return this.$ionic.alertController
                .create({
                    header: "Invalid ZipCode",
                    message: "Please enter a valid US ZipCode",
                    buttons: ["OK"]
                }).then(a => a.present())
        }
    }
}
</script>