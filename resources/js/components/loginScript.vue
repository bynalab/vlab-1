<template>
    <div></div>
</template>
<script>	
	export default {
		data:function() {
		   	return{
                username:"",
                password:"",
                error:"",
		    	}
        },
        methods:{
            singleValidate: function(id){
                $('#'+id).css('border','1px solid #e45');
                $('.requiredv').remove();
                $('#'+id).after('<span class="text-danger requiredv">Required !</span>')
            },
            validateI: function(id,sel=0, psw=false){
                if (sel ===0) {                        
                    let index =-1;                    
                    let $vm = this;
                    
                        if($('#'+id).val() == ""){                            
                            $('#'+id).css('border','1px solid #e45');
                            $('.requiredv').remove();
                            $('#'+id).after('<span class="text-danger requiredv">Required !</span>');
                            return false;
                        }else{
                            return $('#'+id).val();
                        }                                                           
                }
                if (sel=== 1) {
                    if($('#'+id+ 'option:selected').text()==""){
                        $('#'+id).css('border','1px solid #e45');
                        $('.requiredv').remove();
                        $('#'+id).after('<span class="text-danger requiredv">Required !</span>');                       
                        return false                    
                    }else{                      
                        return true;
                    }
                }
            }
        },


        created:function(){		  
        
        	
        },
        mounted(){
            let $vm = this;
            this.$nextTick(function(){
                    $('#matric-number, #password').keyup(function(){
                        $(this).css('border','1px solid #bbb');
                        $(this).next('.requiredv').remove();
                    });
                try{

                }catch(err){
                    
                }

                    $('#login-btn').click(function(){                        
                        $vm.username = $vm.validateI('matric-number');
                        $vm.password = $vm.validateI('password');                    

                        if ($vm.username != "" && $vm.password != "") {
                            
                           /* var formContents = jQuery("#login-form").serialize();
                            */           
                            $('#login-msg').css('display','flex');
                            try{
                                $vm.axios.post('api/login', {email:$vm.username, password:$vm.password}).then(function(response, status, request) {  
                              
                                    localStorage.setItem('LoggedUser',JSON.stringify(response.data));
                                    
                                    /*update store*/
                              //      $vm.$store.commit('updateUser',response);

                                    $('#response-data').val(JSON.stringify(response));
                                    $('#auto-redirect').submit();
                                    $('#login-msg').css('display','none');                                    
                                        
                                 }, function() {
                                    $('#login-msg').css('display','none');                                    
                                    $('#login-err').show();
                                });                                
                            }catch(err){
                                $('#login-msg').css('display','none');
                                $('#login-err2').show();
                            }                 
                        }
                    })

            })
        }
        
	
};
</script>