<template>
<v-container>
    <v-app-bar app color="primary" dark elevation="2" clipped-left fixed>
        <v-row>
            <v-col cols="12" class="">
                <div class="align-center">

                    <v-img alt="Name" class="shrink" contain src="https://i.imgur.com/cSoGQVN.png" height="50" />
                </div>
            </v-col>

        </v-row>

    </v-app-bar>
    <v-row>
        <v-col cols="12" xl="6" lg="8" md="8" sm="8" xs="12" offset-md="2" offset-sm="2" offset-lg="2" offset-xl="3">
            <template>
                <v-card color="primary" class="px-5 py-2 my-5 white--text" v-show="startDate">
                    <v-row>
                        <v-col cols="12" xs="6" xl="3" lg="3" md="3" sm="3"><strong>Check-in : </strong>{{startDate}}</v-col>
                        <v-col cols="12" xs="6" xl="3" lg="3" md="3" sm="3"><strong>Check-Out </strong>{{endDate}}</v-col>
                        <v-col cols="12" xs="6" xl="3" lg="3" md="3" sm="3" v-show="roomType"><strong>Oda Tipi : </strong>{{roomType}}</v-col>
                        <v-col cols="12" xs="6" xl="3" lg="3" md="3" sm="3" v-show="roomView"><strong>Manzara : </strong>{{roomView}}</v-col>
                    </v-row>
                </v-card>
                <v-stepper v-model="e1">
                    <v-stepper-header>
                        <v-stepper-step :complete="e1 > 1" step="1" editable non-linear>Tarih Seçimi</v-stepper-step>

                        <v-divider></v-divider>

                        <v-stepper-step :complete="e1 > 2" step="2" editable>Oda Seçimi</v-stepper-step>

                        <v-divider></v-divider>

                        <v-stepper-step step="3" editable>Ödeme</v-stepper-step>
                    </v-stepper-header>

                    <v-stepper-items>
                        <v-stepper-content step="1">

                            <v-row>
                                <v-col cols="12" xl="3" lg="3" md="3" sm="3" xs="12">
                                    <v-dialog ref="dialog" v-model="modal" :return-value.sync="date" persistent width="290px">
                                        <template v-slot:activator="{ on }">
                                            <v-text-field :rules="[rules.required]" solo v-model="startDate" label="Check-in" append-icon="event" readonly v-on="on">
                                            </v-text-field>
                                        </template>
                                        <v-date-picker v-model="startDate" scrollable locale="tr">
                                            <v-spacer></v-spacer>
                                            <v-btn text color="primary" @click="modal = false">İptal</v-btn>
                                            <v-btn text color="primary" @click="$refs.dialog.save(date)">Tamam</v-btn>
                                        </v-date-picker>
                                    </v-dialog>
                                </v-col>
                                <v-col cols="12" xl="3" lg="3" md="3" sm="3" xs="12">
                                    <v-dialog ref="dialog2" v-model="modal2" :return-value.sync="date" persistent width="290px">
                                        <template v-slot:activator="{ on }">
                                            <v-text-field :rules="[rules.required]" v-model="endDate" label="Check-Out" append-icon="event" readonly v-on="on" solo append-outer-icon></v-text-field>
                                        </template>
                                        <v-date-picker v-model="endDate" scrollable locale="tr">
                                            <v-spacer></v-spacer>
                                            <v-btn text color="primary" @click="modal2 = false">İptal</v-btn>
                                            <v-btn text color="primary" @click="$refs.dialog2.save(date)">Tamam</v-btn>
                                        </v-date-picker>
                                    </v-dialog>
                                </v-col>
                            </v-row>

                            <v-btn color="primary" v-show="endDate" @click="e1 = 2">
                                İleri
                            </v-btn>

                        </v-stepper-content>

                        <v-stepper-content step="2">

                            <h3>
                                Oda Seçimi
                            </h3>
                            <v-divider></v-divider>

                            <v-radio-group v-model="roomType" :rules="[rules.required]">
                                <v-row>
                                    <v-col cols="4">
                                        <v-img src="https://i.pinimg.com/564x/75/a0/56/75a056eec7522a73457856434daf348a.jpg" aspect-ratio="1.2" class="my-3"></v-img>
                                        <v-radio label="Standart" value="Standart"></v-radio>
                                    </v-col>
                                    <v-col cols="4">
                                        <v-img src="https://i.pinimg.com/564x/28/53/f3/2853f3f1d39a3de64b2176994e5c6005.jpg" aspect-ratio="1.2" class="my-3"></v-img>
                                        <v-radio label="Deluxe" value="Deluxe"></v-radio>
                                    </v-col>
                                    <v-col cols="4">
                                        <v-img src="https://i.pinimg.com/564x/a5/22/d2/a522d28ae8a0d9463dca87c2db37e8b8.jpg" aspect-ratio="1.2" class="my-3"></v-img>
                                        <v-radio label="Suit" value="Suit"></v-radio>
                                    </v-col>

                                </v-row>
                            </v-radio-group>

                            <h3>
                                Manzara Seçimi
                            </h3>
                            <v-divider></v-divider>
                            <v-radio-group v-model="roomView">
                                <v-row>

                                    <v-col cols="4">
                                        <v-img src="https://i.pinimg.com/564x/9a/a1/32/9aa132105d61a732ac7ccdad23dd3205.jpg" aspect-ratio="1.2" class="my-3"></v-img>
                                        <v-radio label="Deniz" value="Deniz"></v-radio>
                                    </v-col>
                                    <v-col cols="4">
                                        <v-img src="https://i.pinimg.com/564x/03/53/0c/03530c4121d7f1893727feb4e3751495.jpg" aspect-ratio="1.2" class="my-3"></v-img>
                                        <v-radio label="Kara" value="Kara"></v-radio>
                                    </v-col>

                                </v-row>
                            </v-radio-group>

                            <v-btn color="primary" @click="e1 = 3" v-show="roomView">
                                Devam Et
                            </v-btn>
                        </v-stepper-content>

                        <v-stepper-content step="3">
                            <v-form v-model="isFormValid">
                                <v-container>
                                    <v-row>
                                        <v-col cols="12" xs="12" xl="6" lg="6" md="6" sm="6">
                                            <v-text-field :rules="[rules.ccn]" type="number" max="11" dense label="Kart Numarası" placeholder="**** **** **** ****" counter="11" outlined v-model="cardNo"></v-text-field>
                                            <v-text-field :rules="[rules.cui]" dense outlined label="Kart Üzerindeki İsim" v-model="cui" placeholder=""></v-text-field>
                                            <v-row>
                                                <v-col cols="6">
                                                    <v-text-field :rules="[rules.skt]" dense type="number" outlined label="Son Kullanma Tarihi" v-model="skt" placeholder="MM/YY" counter="4"></v-text-field>
                                                </v-col>
                                                <v-col cols="6">
                                                    <v-text-field :rules="[rules.cvc]" dense type="number" outlined label="Güvenlik Numarası" v-model="cvc" placeholder="CVC" counter="3"></v-text-field>
                                                </v-col>
                                            </v-row>

                                        </v-col>
                                        <v-col cols="12" xs="12" xl="6" lg="6" md="6" sm="6">
                                            <div class="cc">

                                                <div class="ccno">
                                                    {{cardNo}}
                                                </div>
                                                <v-row>
                                                    <v-col cols="6">
                                                        <div class="ccname">{{cui}}</div>

                                                    </v-col>
                                                    <v-col cols="6">
                                                        <div class="cvc text-left">{{skt}}</div>

                                                    </v-col>

                                                </v-row>
                                            </div>
                                        </v-col>
                                    </v-row>
                                </v-container>

                                <v-dialog v-model="dialog" width="500">
                                    <template v-slot:activator="{ on }">
                                        <v-btn @click="pay()" color="primary" dark v-on="on" :disabled="!isFormValid">
                                            Ödeme Yap
                                        </v-btn>
                                    </template>

                                    <v-card>
                                        <v-card-title class="headline primary white--text" primary-title>
                                            Ödemeniz Alınmıştır
                                        </v-card-title>

                                        
                                            <v-alert text type="success">
                                                Bizi tercih ettiğiniz için teşekkür ederiz.
                                            </v-alert>
                                      

                                        <v-card-actions>
                                            <v-spacer></v-spacer>
                                            <v-btn color="primary" text @click="dialog = false">
                                                Kapat
                                            </v-btn>
                                        </v-card-actions>
                                    </v-card>
                                </v-dialog>
                            </v-form>
                        </v-stepper-content>
                    </v-stepper-items>
                </v-stepper>
            </template>
        </v-col>
    </v-row>
</v-container>
</template>

<script>
export default {

    name: 'HelloWorld',

    data: () => ({
        e1: 1,
        date: '',
        startDate: '',
        endDate: '',
        roomType: '',
        roomView: '',
        modal: false,
        modal2: false,
        name: '',
        cardNo: '',
        cui:'',
        max: 11,
        cvc: '',
        skt: '',
        isFormValid: '',
        dialog: false,

        rules: {
            required: value => !!value || 'Boş bırakmayınız.',
            ccn: value => !!value || 'Kredi kartı numaranızı giriniz',
            cui: value => !!value || 'Kart üzerindeki ismi giriniz',
            cvc: value => !!value || 'Kart güvenlik numarasını giriniz',
            skt: value => !!value || 'Kart son kullanma tarihini giriniz',
            counter2: value => value.length != 11 || 'Min 11 characters',
        }
    }),
    mounted() {
        if (localStorage.startDate) this.startDate = localStorage.startDate;
        if (localStorage.endDate) this.endDate = localStorage.endDate;
        if (localStorage.roomType) this.roomType = localStorage.roomType;
        if (localStorage.roomView) this.roomView = localStorage.roomView;
        if (localStorage.cardNo) this.cardNo = localStorage.cardNo;
        if (localStorage.cvc) this.cvc = localStorage.cvc;
        if (localStorage.skt) this.skt = localStorage.skt;
        if (localStorage.cui) this.cui = localStorage.cui;
    },
    methods: {
        pay() {
            localStorage.startDate = this.startDate;
            localStorage.endDate = this.endDate;
            localStorage.roomType = this.roomType;
            localStorage.roomView = this.roomView;
            localStorage.endDate = this.endDate;
            localStorage.cardNo = this.cardNo;
            localStorage.cvc = this.cvc;
            localStorage.skt = this.skt;
            localStorage.cui = this.cui;
            console.log('Ödeme yapılmıştır!!!');
            this.dialog = true;
        }
    }
}
</script>

<style scoped>
.cc {
    background-image: url("https://i.imgur.com/YmIXkeL.jpg");
    background-position: unset;
    height: 220px;
    background-size: 100%;
}

.ccno {
    padding-top: 110px;
    padding-left: 20px;
    color: aliceblue;
    text-shadow: 2px 1px #000;
}

.ccname {
    padding-left: 20px;
    color: aliceblue;
    text-shadow: 2px 1px #000;

}
</style>
