<template>
    <form class='w-[500px]' @submit='handleSubmit($event)'>
        <h2 class='text-gray-700 font-bold text-2xl text-center mb-7'>Form Mahasiswa</h2>
        <div class='flex flex-col mb-3'>
            <label for="nama" class='mb-2 font-medium'>Nama Mahasiswa</label>
            <input 
                type="text" 
                id="nama" 
                placeholder='Input nama mahasiswa...' 
                v-model.trim="formValues.nama" 
                @blur="handleBlur($event)"
                class='p-2 border border-[#ccc] rounded-md'>
            <p class="mt-1 text-red-500 text-sm font-medium" v-show="formErrors.nama">{{formErrors.nama}}</p>
        </div>
        <div class='flex flex-col mb-3'>
            <label for="NIM" class='mb-2 font-medium'>NIM Mahasiswa</label>
            <input 
                type="number" 
                id="NIM" 
                placeholder='Input NIM mahasiswa...' 
                v-model.number="formValues.NIM"
                @blur="handleBlur($event)"
                class='p-2 border border-[#ccc] rounded-md'>
            <p class="mt-1 text-red-500 text-sm font-medium" v-show="formErrors.NIM">{{formErrors.NIM}}</p>
        </div>
        <div class='flex flex-col mb-3'>
            <label for="prodi" class='mb-2 font-medium'>Program Studi</label>
            <select id="prodi" v-model="formValues.prodi" @blur="handleBlur($event)" class='p-2 border border-[#ccc] rounded-md'>
                <option value="" selected>Pilih Program Studi</option>
                <option value="S1 Sistem Informasi">S1 Sistem Informasi</option>
                <option value="S1 Teknologi Informatika">S1 Teknologi Informatika</option>
                <option value="S1 Keperawatan">S1 Keperawatan</option>
                <option value="D3 Keperawatan">D3 Keperawatan</option>
            </select>
            <p class="mt-1 text-red-500 text-sm font-medium" v-show="formErrors.prodi">{{formErrors.prodi}}</p>
        </div>
        <div class="flex mb-3">
            <div class='flex-1 flex flex-col mr-5'>
                <label for="tempatLahir" class='mb-2 font-medium'>Tempat lahir</label>
                <input 
                    type="text" 
                    id="tempatLahir" 
                    placeholder='Input tempat lahir mahasiswa...' 
                    v-model.trim="formValues.tempatLahir"
                    @blur="handleBlur($event)"
                    class='p-2 border border-[#ccc] rounded-md'>
                <p class="mt-1 text-red-500 text-sm font-medium" v-show="formErrors.tempatLahir">{{formErrors.tempatLahir}}</p>
            </div>
            <div class='flex-1 flex flex-col'>
                <label for="tanggalLahir" class='mb-2 font-medium'>Tanggal lahir</label>
                <input 
                    type="date" 
                    id="tanggalLahir" 
                    v-model="formValues.tanggalLahir"
                    @blur="handleBlur($event)"
                    class='p-2 border border-[#ccc] rounded-md'>
                <p class="mt-1 text-red-500 text-sm font-medium" v-show="formErrors.tanggalLahir">{{formErrors.tanggalLahir}}</p>
            </div>
        </div>
        <div class="flex flex-col mb-3">
            <label for="tempatLahir" class='mb-2 font-medium'>Jenis Kelamin</label>
            <div class="flexx">
                <div class="flex mr-5">
                    <input type="radio" id="pria" class="mr-1" value="pria" v-model="formValues.jenisKelamin">
                    <label for="pria">Pria</label>
                </div>
                <div class="flex">
                    <input type="radio" id="perempuan" class="mr-1" value="perempuan" v-model="formValues.jenisKelamin">
                    <label for="perempuan">Perempuan</label>
                </div>
            </div>
            <p class="mt-1 text-red-500 text-sm font-medium" v-show="formErrors.jenisKelamin">{{formErrors.jenisKelamin}}</p>
        </div>
        <div class="flex flex-col mb-3">
            <label for="tempatLahir" class='mb-2 font-medium'>Skills</label>
            <div class="flexx">
                <div class="flex mr-5">
                    <input type="checkbox" id="leadership" class="mr-1" value="leadership" v-model="formValues.skills">
                    <label for="leadership">Leadership</label>
                </div>
                <div class="flex mr-5">
                    <input type="checkbox" id="communication" class="mr-1" value="communication" v-model="formValues.skills">
                    <label for="communication">Communication</label>
                </div>
                <div class="flex mr-5">
                    <input type="checkbox" id="programming" class="mr-1" value="programming" v-model="formValues.skills">
                    <label for="programming">Programming</label>
                </div>
                <div class="flex mr-5">
                    <input type="checkbox" id="design" class="mr-1" value="design" v-model="formValues.skills">
                    <label for="design">Design</label>
                </div>
            </div>
            <p class="mt-1 text-red-500 text-sm font-medium" v-show="formErrors.skills">{{formErrors.skills}}</p>
        </div>
        <div class='flex flex-col mb-3'>
            <label for="motivasi" class='mb-2 font-medium'>Motivasi Anda</label>
            <textarea 
                rows="5"
                id="motivasi" 
                placeholder='Input tempat lahir mahasiswa...' 
                v-model.trim="formValues.motivasi"
                @blur="handleBlur($event)"
                class='p-2 border border-[#ccc] rounded-md'></textarea>
            <p class="mt-1 text-red-500 text-sm font-medium" v-show="formErrors.motivasi">{{formErrors.motivasi}}</p>
        </div>
        <div class='flex flex-col mb-3'>
            <label for="cv" class='mb-2 font-medium'>Upload VC Anda</label>
            <input 
                type="file" 
                id="cv" 
                @blur="handleBlur($event)"
                @change="changeEventFile($event)"
                class='p-2'>
            <p class="mt-1 text-red-500 text-sm font-medium" v-show="formErrors.cv">{{formErrors.cv}}</p>
        </div>
        <div class="flexx space-x-5">
            <button type="submit" class='w-full bg-gradient-to-r from-pink-600 to-fuchsia-600 border-none outline-none p-2 rounded-md text-white font-medium text-lg'>Submit</button>
            <button type="button" class='w-full bg-red-700 border-none outline-none p-2 rounded-md text-white font-medium text-lg' v-on:click="handleReset()">Reset</button>
        </div>
    </form>
</template>


<script>
    function handleErrors(values) {
        let errors = {
            nama: '',
            NIM: '',
            prodi: '',
            tempatLahir: '',
            tanggalLahir: '',
            jenisKelamin: '',
            motivasi: '',
            cv: ''
        }
        if(values.nama === '') {
            errors.nama = 'Field is required'
        } else {
            errors.nama = ''
        }
        if(values.NIM === '') {
            errors.NIM = 'Field is required'
        } else {
            errors.NIM = ''
        }
        if(values.prodi === '') {
            errors.prodi = 'Field is required'
        } else { 
            errors.prodi = ''
        }
        if(values.tempatLahir === '') {
            errors.tempatLahir = 'Field is required'
        } else {
            errors.tempatLahir = ''
        }
        if(values.tanggalLahir === '') {
            errors.tanggalLahir = 'Field is required'
        } else {
            errors.tanggalLahir = ''
        }
        if(values.jenisKelamin === '') {
            errors.jenisKelamin = 'Field is required'
        } else {
            errors.jenisKelamin = ''
        }
        if(values.skills.length === 0) {
            errors.skills = 'Field is required'
        } else {
            errors.skills = ''
        }
        if(values.motivasi === '') {
            errors.motivasi = 'Field is required'
        } else {
            errors.motivasi = ''
        }

        if(values.cv === '' || values.cv === null) {
            errors.cv = 'Field is required'
        } else {
            errors.cv = ''
        }

        return errors
    }

    export default {
        data() {
            return {
                formValues: {
                    nama: '',
                    NIM: '',
                    prodi: '',
                    tempatLahir: '',
                    tanggalLahir: '',
                    jenisKelamin: '',
                    motivasi: '',
                    skills: [],
                    cv: ''
                },
                formErrors: {
                    nama: '',
                    NIM: '',
                    prodi: '',
                    tempatLahir: '',
                    tanggalLahir: '',
                    jenisKelamin: '',
                    motivasi: '',
                    skills: '',
                    cv: ''
                }
            }
        },
        methods: {
            //this method for handling input file
            changeEventFile(event) {
                this.formValues.cv = event.target.files[0]
            },
            //this method for handling blur input (except checkbox and radio)
            handleBlur(event) {
                //when value is empty, will give error on input
                if(event.target.value === '') {
                    this.formErrors[event.target.id] = 'Field is required'
                } else {
                    //and when value is filled. Error will disappeared
                    this.formErrors[event.target.id] = ''
                }
            },  
            //this method for handling submit
            handleSubmit(event) {
                event.preventDefault()
                //handling errros every submit
                const errors = handleErrors(this.formValues)
                this.formErrors = errors
                //check if every errors is empty
                if(Object.values(this.formErrors).every(v => v === '')) {
                    this.formValues.NIM = this.formValues.NIM.toString()
                    console.log(this.formValues.nama)
                    console.log(this.formValues.NIM)
                    console.log(this.formValues.prodi)
                    console.log(this.formValues.tempatLahir)
                    console.log(this.formValues.tanggalLahir)
                    console.log(this.formValues.jenisKelamin)
                    console.log(this.formValues.motivasi)
                    console.log(this.formValues.skills)
                    console.log(this.formValues.cv)
                } 
            },
            //this method for handling reset values form 
            handleReset() {
                Object.keys(this.formValues).forEach(key => {
                    this.formValues[key] = key === 'skills' ? [] : ''
                    this.formErrors[key] = ''
                })
                document.getElementById('cv').value = ''
            },
        }
    }
</script>
