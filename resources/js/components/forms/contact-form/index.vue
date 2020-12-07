<template>
  



<!-- Load Facebook SDK for JavaScript -->
      <div id="fb-root"></div>
    

      <!-- Your Chat Plugin code -->
      <div class="fb-customerchat"
        attribution=setup_tool
        page_id="173001153127662"
  logged_in_greeting="Bienvenido, ¿Cuéntanos en que podemos ayudarte?"
  logged_out_greeting="Bienvenido, ¿Cuéntanos en que podemos ayudarte?">
      </div>




</template>

<script>


        window.fbAsyncInit = function() {
          FB.init({
            xfbml            : true,
            version          : 'v9.0'
          });
        };

        (function(d, s, id) {
        var js, fjs = d.getElementsByTagName(s)[0];
        if (d.getElementById(id)) return;
        js = d.createElement(s); js.id = id;
        js.src = 'https://connect.facebook.net/es_LA/sdk/xfbml.customerchat.js';
        fjs.parentNode.insertBefore(js, fjs);
      }(document, 'script', 'facebook-jssdk'));












export default {
    props:["offer"],

    data(){
        return {
            fullName:"",
            email:"",
            phone:"",
            baseUrl:baseUrl,
            disableButton:false,
            captcha:"",
        }
    },

    methods:{
        /*
        verifyCaptcha(captcha){
            this.captcha=captcha;
        },

        onCaptchaError(err){
            console.log("error captcha ", err)
            toastr.error("error en la validación del captcha, comprueba tu conexión a internet e intenta nuevamente")
        },

        onCaptchaExpired(err){
            console.log("error captcha ", err)
            toastr.error("el captcha se expiró, intente nuevamente")
        },*/

        getFullRound(){
            if(!this.offer) return "consult-card-full-rounded";
            else return "col-lg-5 col-xl-5 col-12";
        },
        sendMail(){

            let fd= new FormData();

            if(this.fullName&&this.fullName!="") fd.append("fullName", this.fullName);
            else return toastr.error("Rellene todos los campos");
            if(this.email&&this.email!="") fd.append("email", this.email);
            else return toastr.error("Rellene todos los campos");
            if(this.phone&&this.phone!="") fd.append("phone", this.phone);
            else return toastr.error("Rellene todos los campos");

            //if(this.captcha&&this.captcha!="") fd.append("g-recaptcha-response", this.captcha);
            //else return toastr.error("Complete la prueba de captcha");

            if(this.offer){
                fd.append("offer", this.offer.id)
                fd.append("type", "offer")
                fd.append("company_name", this.offer.company_name)
                fd.append("service_name", this.offer.service_name)
                if(this.offer.department) fd.append("department", this.offer.department_name)
                if(this.offer.municipality) fd.append("municipality", this.offer.municipality_name)
            }

            fd.append("type", this.offer?"offer":"general");

            this.disableButton= true;

            let loader = this.$loading.show();

            axios.post(baseUrl+"/api/mail/contact", fd)
            .then(res=>{
                console.log("server response ",res);
                toastr.success("Datos enviados exitosamente");
            }).catch(err=>{
                console.log("server error ",err.response);
                toastr.error("Error al enviar los datos, intente nuevamente");
            })
            .finally(()=>{
                this.disableButton=false;
                loader.hide()
            });
        }
    },

    computed:{

        reCaptchaKey: {
            get(){
                return window.reCaptchaKey;
            }
        },

    }
}
</script>

<style>

.v-captcha{
    transform: scale(0.7);
    -webkit-transform: scale(0.7);
    transform-origin: 0 0;
    -webkit-transform-origin: 0 0;
}

@media (max-width:350px) {
    .v-captcha{
        transform: scale(0.6);
        -webkit-transform: scale(0.6);
    }
}

</style>
