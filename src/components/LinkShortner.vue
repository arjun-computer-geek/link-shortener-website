<!-- scripts -->
<script>
import Clipboard from 'v-clipboard'
export default {
    data() {
        return {
            url: null,
            api_key: '8a5e42cf9d92672e35f8729c105cf8ce5f30a3a4',
            link: null,
            err: null
        }
    },
    methods: {
        async submit() {

            this.clearError()
            const requestOptions = {
                method: "POST",
                headers: { Authorization: `Bearer ${this.api_key}`, "Content-Type": "application/json" },
                body: JSON.stringify({ long_url: this.url, domain: 'bit.ly' })
            };
            const response = await fetch("https://api-ssl.bitly.com/v4/shorten", requestOptions);
            const data = await response.json();
            if (response.ok) {
                this.link = data.link
            }
            else {
                this.err = data.description
            }
        },
        clearError() {
            this.err = null
        }


    }
}
</script>

<!-- views -->
<template>
    <div class="container">
        <h1>Link Shortner</h1>
        <input v-model="url" type="text" v-on:input="clearError" placeholder="Paste your link" />
        <p v-if="err" class="err">{{ err }}</p>
        <button class="btn" @click.prevent="submit">Submit</button>
        <input v-if="link" type="text" :value="link" />
    </div>
</template>

<style scoped>
.container {
    min-height: 80vh;
    width: 60%;
    margin: auto;
    margin-top: 50px;
    padding: 50px;
    text-align: center;
    border-radius: 20px;
    box-shadow: rgba(50, 50, 93, 0.25) 0px 50px 100px -20px, rgba(0, 0, 0, 0.3) 0px 30px 60px -30px;
}

input {
    display: block;
    padding-bottom: 5px;
    margin: auto;
    width: 60%;
    text-align: center;
    border: none;
    border-bottom: 2px solid grey;
}

input:focus {
    outline: none;
    border-bottom: 2px solid rgb(127, 255, 127);
}

.btn {
    margin-top: 20px;
    margin-bottom: 20px;
    background-color: rgb(13, 10, 31);
    border: none;
    color: white;
    padding: 10px 20px;
    border-radius: 5px;
    cursor: pointer;
    font-weight: bold;
}

.btn:hover {
    background-color: rgba(13, 10, 31, 0.8);
}

.err {
    color: "red"
}

/* mobiel media query */
@media only screen and (max-width: 600px) {
    .container {
        min-height: 90vh;
        width: 80%;
        margin-top: 30px;
        padding: 20px;
    }

    input {
        width: 90%;
    }
}
</style>