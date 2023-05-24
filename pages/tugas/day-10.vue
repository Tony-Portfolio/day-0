<template>
    <div class="bg-[#e2e9f4] w-full">
        <NuxtLayout :name="layouts.header"></NuxtLayout>
        <main class="w-10/12 mx-auto my-8 flex gap-2 flex-col">
            <section>
                <div class="bg-white rounded p-4">
                    <div class="flex gap-2 flex-col">
                        <h3>Tugas 1:</h3>
                        <label class="text-base text-black/[0.6]" for="text">Masukkan kalimat atau teks:</label>
                        <div class="flex gap-2">

                            <input type="text" id="text" class="border-2 border-black/[0.1] py-1 rounded p-2"
                                v-model="text" />
                            <button class="bg-sky-500 rounded text-white p-2 py-1" @click="tampilkan">Kirim</button>
                        </div>
                        <p>Hasil: <span v-html="result"></span></p>
                    </div>
                </div>
            </section>
            <hr>
            <section>
                <div class="bg-white rounded p-4">
                    <div class="flex gap-2 flex-col">
                        <h3>Tugas 2:</h3>
                        <div>Array: [ <span v-for="item in inputArray" :key="item.name">{"name":"{{ item.name }}","age": {{ item.age }}}, <br></span>]</div>
                        <div>Array: [ <span v-for="item in filterArray" :key="item.name">{"name":"{{ item.name }}","age": {{ item.age }}}, <br></span>]</div>
                    </div>
                </div>
            </section>
            <hr>
            <section>
                <div class="bg-white rounded p-4">
                    <div class="flex gap-2 flex-col">
                        <h3>Tugas 3:</h3>
                        <label class="text-base text-black/[0.6]" for="numbers">Masukkan Angka (format: 1,2,3,4,5)</label>
                        <div class="flex gap-2">
                            <input type="text" id="numbers" class="border-2 border-black/[0.1] py-1 rounded p-2"
                                v-model="text_3" />
                            <button class="bg-sky-500 rounded text-white p-2 py-1" @click="tampilkan_3">Kirim</button>
                        </div>
                        <p>Hasil: <span v-html="result_3"></span></p>
                    </div>
                </div>
            </section>
        </main>
        <NuxtLayout :name="layouts.footer"></NuxtLayout>
    </div>
</template>
  
<script>
export default {
    data() {
        return {
            layouts: {
                header: "header",
                footer: "footer",
            },
            result: "",
            result_2: "",
            result_3: "",
            text: "",
            text_3: "",
            inputArray: [
                { name: "Sophia", age: 41 },
                { name: "James", age: 33 },
                { name: "Olivia", age: 46 },
                { name: "Bob", age: 30 },
                { name: "Emma", age: 47 },
                { name: "James", age: 32 },
                { name: "Emma", age: 37 },
                { name: "Emma", age: 41 },
                { name: "John", age: 13 },
                { name: "Jane", age: 11 },
                { name: "John", age: 37 },
                { name: "Bob", age: 20 },
                { name: "Emma", age: 18 },
                { name: "William", age: 5 },
                { name: "Jane", age: 1 },
            ],
            filterArray: []
        };
    },
    methods: {
        separate(text) {
            if (text === "") {
                this.result = "";
            } else {
                const textSplit = text.split(" ");
                const separate = textSplit.map((word) => word.split("").join("@"));
                const output = separate.join(" ");
                this.result = output;
            }
        },
        tampilkan() {
            this.separate(this.text);
        },
        sortarray() {
            this.inputArray.sort((a, b) => a.name.localeCompare(b.name));
            const noDup = {};
            this.filterArray = this.inputArray.filter((a) => {
                if (!noDup[a.name]) {
                    noDup[a.name] = true;
                    return true;
                }
                return false;
            });
        },
        calcnumber() {
            const operasiNilai = (array) => {
                let total = 0;
                return array.map((num) => {
                    total += num;
                    return total;
                });
            };

            const numbers = this.text_3.split(",").map((num) => parseInt(num.trim()));
            const result = operasiNilai(numbers);
            this.result_3 = result.join(", ");
        },
        tampilkan_3() {
            this.calcnumber();
        },
    },
    mounted() {
        this.separate(this.text);
        this.sortarray();
    },
};
</script>
  