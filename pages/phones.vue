<template>
    <div>
        <NavBar />

        <div class="container">
            <EditPhoneModal :phone="selectedPhone" />
            <DeletePhoneModal :phone="selectedPhone" @onDeleted="getAll" />
            
            <h1>
                <PhoneEntryModal class="float-right" @onAdd="getAll" />
                Phone
            </h1>

            <table class="table table-boredered">
                <thead>
                    <tr class="bg-info text-white">
                        <th>Phone Name</th>
                        <th>Description</th>
                        <th>Ram</th>
                        <th>Battery</th>
                        <th>Price</th>
                        <th>&nbsp;</th>
                        <th>&nbsp;</th>
                    </tr>
                </thead>

                <tbody>
                    <tr v-for="phone in phones" :key="phone.id">
                        <td>{{phone.phone_name}}</td>
                        <td>{{phone.description}}</td>
                        <td>{{phone.ram}}</td>
                        <td>{{phone.battery}}</td>
                        <td>{{phone.price}}</td>
                        <td>
                            <b-button @click="onEdit(phone)" variant="info" size="sm">Edit</b-button>
                        </td>
                        <td>
                            <b-button @click="onDelete(phone)" variant="danger" size="sm">Delete</b-button>
                        </td>
                    </tr>
                </tbody>

            </table>

        </div>

    </div>
</template>

<script>
export default {
    data() {
        return {
            phones: [],
            selectedPhone: {}
        }
    },
    methods: {
        async getAll() {
            await this.$axios.get('http://localhost:8000/api/phones')
            .then((res)=>{
                if(res.status==200) {
                    this.phones = res.data
                    console.log(this.phones)
                }
            })
        },
        onEdit(selectedPhone) {
            this.selectedPhone = selectedPhone;
            this.$bvModal.show('editPhoneModal')
        },
        onDelete(selectedPhone) {
            this.selectedPhone = selectedPhone;
            this.$bvModal.show('deletePhoneModal')
        }
    },
    created() {
        this.getAll()
    }
}
</script>