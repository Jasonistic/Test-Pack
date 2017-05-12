# Test-Pack
#Animation pour une présentation de tarifs suivant conditions
#Bonjour! Grand débutant en POO et JS/Jquery j'ai commis ce script qui comporte des bugs. J'affichais dans une bulle deux tarifs, un #vide et un meublé pour deux formules. J'ai ajouté un deuxième groupe de choix, suivant que le tarif à afficher est mensuel (par défaut) #ou annuel. Et là je n'ai plus rien... Mes ajouts figurent en commentaire de ce code. Merci de votre aide!

$(document).ready(function() {
    // placement de la bulle au chargement de la page
    var control = $('input[type="range"]'),
        controlMin = control.attr('min'),
        controlMax = control.attr('max'),
        controlVal = control.val(),
        controlThumbWidth = control.data('thumbwidth'),

        output = $('output'),

        outputLoyer = $('#loyer'),
        loyer = $('#loyer > p'),

        formuleIntegraleM = $('#formuleIntegraleM > p'),
        formuleEssentielleM = $('#formuleEssentielleM > p'),
		
		formuleIntegraleA = $('#formuleIntegraleA > p'),
        formuleEssentielleA = $('#formuleEssentielleA > p'),
		
        radios = $('input[type=radio][name=location]'),
        radiosVide = $('input[type=radio][name=location][value=vide]'),
		radiosMeublee = $('input[type=radio][name=location][value=meublee]'),
		
        //declarer un autre groupe de boutons radios
		
		radiosAnnuel= $('input[type=radio] [name=prime][value=annuel]'),
		radiosMensuel = $('input[type=radio] [name=prime][value=mensuel]'),
	

        range = controlMax - controlMin,

        position = ((controlVal - controlMin) / range) * 100,

        positionOffset = Math.round(controlThumbWidth * position / 100) - (controlThumbWidth / 2);

    console.log(output);

    output
        .css('left', 'calc(' + position + '% - ' + positionOffset + 'px)');

    outputLoyer
        .css('left', 'calc(' + position + '% - ' + positionOffset + 'px)');

    $('#min').hide();

    loyer
        .text(tarifPack.loyerBase[0] + ' €');
		
	//loyer
	// .text(tarifPack2.loyerAnnuel[0] + ' €');

    formuleIntegraleM
        .text(tarifPack.formuleIntegraleM.vide[0] + ' €');

    formuleEssentielleM
        .text(tarifPack.formuleEssentielleM.vide[0] + ' €');
		
	formuleIntegraleA
        .text(tarifPack2.formuleIntegraleA.vide[0] + ' €');

    formuleEssentielleA
        .text(tarifPack2.formuleEssentielleA.vide[0] + ' €');
		
		

    // au check d'un radio
    radios.change(function () {

        var controlVal = control.val(),
            tarifIndexOf = tarifPack.loyerBase.indexOf(parseFloat(controlVal));
					

        var value = this.value;

        // Si le radio vide est checked
      if (value === 'vide') {

            formuleIntegraleM
                .text(tarifPack.formuleIntegraleM.vide[tarifIndexOf] + ' €');

            formuleEssentielleM
                .text(tarifPack.formuleEssentielleM.vide[tarifIndexOf] + ' €');

        }
        /* Si le radio meublee est checked
        else if (value === 'meublee') {
            
				
			formuleIntegraleM
                .text(tarifPack.formuleIntegraleM.meublee[tarifIndexOf] + ' €');

            formuleEssentielleM
                .text(tarifPack.formuleEssentielleM.meublee[tarifIndexOf] + ' €');
        }
		 check du bouton radio annuel
		
	
				
		 if (value === 'annuel')&&(value===vide) {
			 
		 var tarifPack = var tarifPack2;

            formuleEssentielleM
                .text(tarifPack2.formuleIntegraleA.vide[tarifIndexOf] + ' €');

            formuleEssentielleM
                .text(tarifPack2.formuleEssentielleA.vide[tarifIndexOf] + ' €');
		 }
			else if (value === 'annuel')&&(value==='meublee') {
           
		   formuleIntegraleA
                .text(tarifPack2.formuleIntegraleA.meublee[tarifIndexOf] + ' €');

            formuleEssentielleM
                .text(tarifPack2.formuleEssentielleA.meublee[tarifIndexOf] + ' €');
        }*/
        
       
       
       

	});

    
    // deplacement de la bulle et affichage du loyer et tarif évolutif
    control.on('input', function () {

        var controlMin = $(this).attr('min'),
            controlMax = $(this).attr('max'),
            controlVal = $(this).val(),
            controlThumbWidth = $(this).data('thumbwidth');

        var range = controlMax - controlMin;

        var position = ((controlVal - controlMin) / range) * 100;

        var positionOffset = Math.round(controlThumbWidth * position / 100) - (controlThumbWidth / 2);

        output
            .css('left', 'calc(' + position + '% - ' + positionOffset + 'px)');

        var tarifIndexOf = tarifPack.loyerBase.indexOf(parseFloat(controlVal));

        if (tarifPack.loyerBase[tarifIndexOf] == parseFloat($('#min').text())) {
            $('#min').hide();
        } else {
            $('#min').show();
        }

        if (tarifPack.loyerBase[tarifIndexOf] == parseFloat($('#max').text())) {
            $('#max').hide();
        } else {
            $('#max').show();
        }

        outputLoyer
            .css('left', 'calc(' + position + '% - ' + positionOffset + 'px)');

        loyer
            .text('Jusqu\'\à '+ tarifPack.loyerBase[tarifIndexOf] + ' €');

        // Si le radio vide est checked
        if (radiosVide.prop( "checked" )) {

            formuleIntegraleM
                .text(tarifPack.formuleIntegraleM.vide[tarifIndexOf] + ' €');

            formuleEssentielleM
                .text(tarifPack.formuleEssentielleM.vide[tarifIndexOf] + ' €');

        }
        // Si le radio meublee est checked
        else if (radiosMeublee.prop( "checked" )) {
           
		   formuleIntegraleM
                .text(tarifPack.formuleIntegraleM.meublee[tarifIndexOf] + ' €');

            formuleEssentielleM
                .text(tarifPack.formuleEssentielleM.meublee[tarifIndexOf] + ' €');
        
		}
		
		/*if (radiosAnnuel.prop("checked"))&&(radiosVide.prop( "checked" )){
			var tarifPack = var tarifPack2;
		
		formuleEssentielleM
                .text(tarifPack2.formuleIntegraleA.vide[tarifIndexOf] + ' €');

            formuleEssentielleM
                .text(tarifPack2.formuleEssentielleA.vide[tarifIndexOf] + ' €');
	}
			else if (radiosAnnuel.prop("checked"))&&(radiosMeublee.prop( "checked" )) {
           
		   formuleIntegraleA
                .text(tarifPack2.formuleIntegraleA.meublee[tarifIndexOf] + ' €');

            formuleEssentielleM
                .text(tarifPack2.formuleEssentielleA.meublee[tarifIndexOf] + ' €');
        }
      */  
    });


});
	
var tarifPack = {
    loyerBase: [400,500,600,700,800,900,1000,1100,1200,1300,1400,1500,1600,1700,1800,1900,2000],

    
    formuleEssentielleM: {
        vide: ['12,25','16,00','19,50','23,00','26,50','30,00','33,50','37,00','40,50','44,00','47,50','51,00','54,50','58,00','61,50','65,00','68,50'], 
        meublee: ['13,50','17,50','21,33','25,25','29,00','33,00','36,80','40,75','44,50','48,30','52,25','56,00','59,80','63,75','67,50','71,50','75,00'],
    },
	formuleIntegraleM: {
        vide: ['14,00','18,00','22,00','26,00','30,00','34,00','38,00','42,00','46,00','50,00','54,00','58,00','62,00','66,00','70,00','74,00','78,00'],
        meublee: ['15,00','19,40','23,70','28,00','32,30','36,60','41,00','45,30','49,60','54,00','58,30','62,60','67,00','71,30','75,60','80,00','84,30']
    }

	};


var tarifPack2 = {
    loyerBase: [400,500,600,700,800,900,1000,1100,1200,1300,1400,1500,1600,1700,1800,1900,2000],

      formuleEssentielleA: {
        vide: [147,192,234,276,318,360,402,444,486,528,570,612,654,696,738,780,822],
	  meublee: [162,210,256,303,348,396,441.60,489,534,579.60,627,672,717.60,765,810,858,900]},
	  
    
	formuleIntegraleA: {
        vide: [168,216,264,312,360,408,456,504,552,600,648,696,744,792,840,888,936],
        meublee: [180,232.80,284.40,336,387.60,439.20,492,543.60,595.20,648,699.60,751.20,804,855.60,907.20,960,1011.60]
	}   
   };
