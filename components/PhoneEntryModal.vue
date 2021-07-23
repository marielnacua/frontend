<template>
    <div>
        <b-button v-b-modal.phoneEntryModal class="btn btn-info">Add Phone</b-button>

        <b-modal id="phoneEntryModal" title="Phone Entry" ok-title="Save" @ok="onSubmit">
            <form action="#" ref="form">
                <b-form-group
                    label="Phone Name"
                    label-for="phone_name"
                    >
                    <b-form-input id="phone_name" v-model="phone.phone_name" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="Description"
                    label-for="description"
                    >
                    <b-form-input id="description" v-model="phone.description" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="Ram"
                    label-for="ram"
                    >
                    <b-form-input id="ram" v-model="phone.ram" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="Battery"
                    label-for="battery"
                    >
                    <b-form-input id="battery" v-model="phone.battery" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="Price"
                    label-for="price"
                    >
                    <b-form-input id="price" type="number" v-model="phone.price" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="Date"
                    label-for="acquired_on"
                    >
                    <b-form-input id="acquired_on" type="date" v-model="phone.acquired_on" trim></b-form-input>
                </b-form-group>

            </form>
        </b-modal>
    </div>
</template>

<script>
export default {
    data() {
        return {
            phone: {},
        }
    },
    methods: {
        async onSubmit() {
            this.$axios.post('http://localhost:8000/api/phones', this.phone)
            .then((res)=>{
                if(res.status==202) {
                    alert('Successfully added the phone')
                    this.$emit('onAdd')
                }
            })
        }
    }
    
}
</script>