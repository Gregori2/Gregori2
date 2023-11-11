<html>
<head>
<title>Kalkulator  do obliczania regresji. Dopasowanie szeregu Fouriera, wielomianowego, i przedziału ufności.</title>
	<script>
jQuery(window).on('load',  function() {
				new JCaption('img.caption');
			});
	var big        = '72%';
	var small      = '53%';
	var bildauf    = '/templates/beez3/images/plus.png';
	var bildzu     = '/templates/beez3/images/minus.png';
	var rightopen  = 'Otwórz informacje';
	var rightclose = 'Zamknij informacje';
	var altopen    = 'jest otwarty';
	var altclose   = 'jest zamknięty';

;(function() { var _menuInit = function() { new Ext.ux.Menu("ariext108", {"transitionDuration":0.2}); Ext.get("ariext108").select(".ux-menu-sub").removeClass("ux-menu-init-hidden"); }; if (!Ext.isIE || typeof(MooTools) == "undefined" || typeof(MooTools.More) == "undefined") Ext.onReady(_menuInit); else window.addEvent("domready", _menuInit); })();
jQuery(document).ready(function(){
    jQuery(".nlevel-menu").smartmenus({
        subMenusSubOffsetX: 1,
        subMenusSubOffsetY: -8,
        showDuration:300
    });
});
jQuery(document).ready(function(){
    jQuery(".nlevel-menu").smartmenus({
        subMenusSubOffsetX: 1,
        subMenusSubOffsetY: -8,
        showDuration:300
    });
});
	</script>	
<script type="text/javascript">
	var tops;
	var diff = 95;
	var leftSlide = 400;
	
	if ( jQuery( ".mobile_sticky" ).length ) {
		offset = jQuery('.mobile_sticky').offset();
		fromTop = offset.top;	

		jQuery(window).scroll(function(e){    
			scroll = jQuery(window).scrollTop();    	
			if(scroll > fromTop){
				jQuery('.mobile_sticky').find('.menu_icon').addClass('topFix');		
			}else{
				jQuery('.mobile_sticky').find('.menu_icon').removeClass('topFix');					
			}
		})	
	}
	/* for normal menu start */
	jQuery('.havechild').hover(function(){		
			
		jQuery(this).find('.have-content').first().css('display','block');					
		jQuery(this).find('.have-content').first().css('position','absolute');
		level = jQuery(this).find('.have-content').attr('level');		
		width = jQuery(this).width();
		height = jQuery(this).height()+6;

		if((level-2) > 0)
			jQuery(this).find('.have-content').first().css('margin','-'+height+'px 0 0 '+width+'px');
				
		jQuery(this).find('.level-'+level).each(function(){
			jQuery(this).css('display','block');
		})

	});

	jQuery('.havechild').mouseleave(function() {		
		jQuery(this).find('.have-content').css('display','none');						
	});

	/* for normal menu end*/		


	/* for responcive menu */

	jQuery(document).ready(function(){

		jQuery( window ).resize(function() {
			setView()			
		});
		jQuery('#yt-off-resmenu').appendTo('html');
		
		defaultOpen();
		setView();

		//make ordering of all ul for mobile view		
		for(i = (jQuery('.mm-list').length-1); i >= 0 ;i--){
			jQuery(this).find('#ul_header').after(jQuery('#mm-'+i+''));
		}		
	});

	jQuery('#mobile_menu_hide').click(function(){	
		
		jQuery('body').animate({left:"0"},800);	
		
		jQuery('#yt-off-resmenu').animate(
			{width:0},
			800,
			function() {
				jQuery('#yt-off-resmenu').removeClass('mm-opened');
				jQuery('#yt-off-resmenu').removeClass('mm-current');
				jQuery('#yt-off-resmenu').addClass('mm-offcanvas');	
				jQuery('body').removeClass('body-position');		
		});
		
		jQuery('body').css({'overflow': 'auto','height': 'auto'});
		//jQuery('body').css('left','0px');		
	});

	jQuery('#mobile_menu_show').click(function(){	
		
		window.scrollTo(0, 0);
		jQuery('#yt-off-resmenu').css('width','0px')		
		
		aa = jQuery( window ).width();
		if( ((aa*diff)/100) > leftSlide )
			aa=leftSlide;
		else
			aa=parseInt((aa*diff)/100);
		aa += 10;
		console.log(aa);

		jQuery('body').animate({left:aa},800);


		jQuery('body').addClass('body-position');		

		aa = jQuery( window ).width();
		if( ((aa*diff)/100) > leftSlide )
			aa=leftSlide;
		else
			aa=diff+'%';


		jQuery('#yt-off-resmenu').animate(
			{width:aa},
			800,
			function() {
				jQuery('#yt-off-resmenu').addClass('mm-opened');				
				jQuery('body').css({'overflow': 'hidden','height': '100%'});
				defaultOpen();								
		});

		jQuery('#yt-off-resmenu').addClass('mm-current');
		jQuery('#yt-off-resmenu').removeClass('mm-offcanvas');		

		return false;
	});				

	jQuery('.mm-subopen').click(function(){
		if('mm-0' == jQuery(this).parent().parent().attr('id') ){
			jQuery('.mm-list').each(function(){
				if('mm-0' == jQuery(this).attr('id') ){

				}else{
					jQuery(this).removeClass('mm-current');
					jQuery(this).removeClass('mm-subopened');
					jQuery(this).removeClass('mm-opened');	
					jQuery(this).removeClass('mm-highest');	
					jQuery(this).addClass('mm-hidden');
				}				
			})
		}

		

		currentUl = jQuery(this).attr('href');
		
		jQuery(currentUl).removeClass('mm-hidden');				
		jQuery(currentUl).addClass('mm-current');
		
		jQuery(currentUl).animate(
			{width:'100%'},
			100,
			function() {
				jQuery(currentUl).addClass('mm-opened');											
		});
		return false;
		
	})

	jQuery('.mm-subclose').click(function(){
		jQuery(this).parent().parent().removeClass('mm-current');				
		id = jQuery(this).parent().parent().attr('id');

		jQuery('#'+id).removeAttr("style");
		jQuery('#'+id).css('top',tops);
		jQuery('#'+id).removeClass('mm-opened');				
		currentUl = jQuery(this).attr('href');
		jQuery(currentUl).addClass('mm-current');			
		jQuery(currentUl).removeClass('mm-subopened');

		setTimeout(function() { jQuery('#'+id).addClass('mm-hidden'); }, 500);

		/*jQuery('#'+id).animate(
			{left:'700px'},
			700,
			,
			function(){															
				jQuery('#'+id).removeAttr("style");
				jQuery('#'+id).css('top',tops);
				jQuery('#'+id).removeClass('mm-opened');
				jQuery('#'+id).addClass('mm-hidden');
				currentUl = jQuery(this).attr('href');
				jQuery(currentUl).addClass('mm-current');			
				jQuery(currentUl).removeClass('mm-subopened');
			}
	);	*/			
		return false;
	})

	function setView(){

		//if(jQuery( window ).width() > 980){
		if(jQuery( window ).width() > 720){	
			if(jQuery('#yt-off-resmenu').hasClass('mm-offcanvas') == false){				
				jQuery('#mobile_menu_hide').click();
			}			
			jQuery('#mobile_menu_show').hide();
			jQuery('#rain_main_ul').show();
			
		}else{
			jQuery('#rain_main_ul').hide();
			jQuery('#mobile_menu_show').show();
		}

	}

		function defaultOpen(){

		fistTab = jQuery('#mm-0');
		
		jQuery('.mm-list').each(function(){		
			jQuery(this).removeClass('mm-current');
			jQuery(this).removeClass('mm-subopened');
			jQuery(this).removeClass('mm-opened');	
			jQuery(this).removeClass('mm-highest');	
			jQuery(this).addClass('mm-hidden');							
		})
				
		currentUl = fistTab;//jQuery(fistTab).attr('href');
		jQuery(currentUl).addClass('mm-current');	
		jQuery(currentUl).addClass('mm-opened');
		jQuery(currentUl).removeClass('mm-hidden');

		currentUl = jQuery('#mm-1');
		jQuery(currentUl).addClass('mm-current');	
		jQuery(currentUl).addClass('mm-opened');
		jQuery(currentUl).removeClass('mm-hidden');
				
		aa = jQuery( window ).width();
		if( ((aa*diff)/100) > leftSlide )
			aa=leftSlide;
		else
			aa=parseInt((aa*diff)/100);

		divWidth = jQuery('#yt-off-resmenu').width();
		totalWidth = 0;
		liHeight = 0;
		jQuery('#mm-0 li').each(function(){			
			totalWidth  = totalWidth+jQuery(this).width();
			liHeight = jQuery(this).height();
		});

		row = totalWidth/divWidth;
		row = parseInt(row)+1;
		tops = (row * liHeight)+40;		
		jQuery('.mm-menu > .mm-panel').css('top',tops+'px');
		
	}	

</script>
<script type="text/javascript">
	var tops;
	var diff = 95;
	var leftSlide = 400;
	
	if ( jQuery( ".mobile_sticky" ).length ) {
		offset = jQuery('.mobile_sticky').offset();
		fromTop = offset.top;	

		jQuery(window).scroll(function(e){    
			scroll = jQuery(window).scrollTop();    	
			if(scroll > fromTop){
				jQuery('.mobile_sticky').find('.menu_icon').addClass('topFix');		
			}else{
				jQuery('.mobile_sticky').find('.menu_icon').removeClass('topFix');					
			}
		})	
	}
	/* for normal menu start */
	jQuery('.havechild').hover(function(){		
			
		jQuery(this).find('.have-content').first().css('display','block');					
		jQuery(this).find('.have-content').first().css('position','absolute');
		level = jQuery(this).find('.have-content').attr('level');		
		width = jQuery(this).width();
		height = jQuery(this).height()+6;

		if((level-2) > 0)
			jQuery(this).find('.have-content').first().css('margin','-'+height+'px 0 0 '+width+'px');
				
		jQuery(this).find('.level-'+level).each(function(){
			jQuery(this).css('display','block');
		})

	});

	jQuery('.havechild').mouseleave(function() {		
		jQuery(this).find('.have-content').css('display','none');						
	});

	/* for normal menu end*/		


	/* for responcive menu */

	jQuery(document).ready(function(){

		jQuery( window ).resize(function() {
			setView()			
		});
		jQuery('#yt-off-resmenu').appendTo('html');
		
		defaultOpen();
		setView();

		//make ordering of all ul for mobile view		
		for(i = (jQuery('.mm-list').length-1); i >= 0 ;i--){
			jQuery(this).find('#ul_header').after(jQuery('#mm-'+i+''));
		}		
	});

	jQuery('#mobile_menu_hide').click(function(){	
		
		jQuery('body').animate({left:"0"},800);	
		
		jQuery('#yt-off-resmenu').animate(
			{width:0},
			800,
			function() {
				jQuery('#yt-off-resmenu').removeClass('mm-opened');
				jQuery('#yt-off-resmenu').removeClass('mm-current');
				jQuery('#yt-off-resmenu').addClass('mm-offcanvas');	
				jQuery('body').removeClass('body-position');		
		});
		
		jQuery('body').css({'overflow': 'auto','height': 'auto'});
		//jQuery('body').css('left','0px');		
	});

	jQuery('#mobile_menu_show').click(function(){	
		
		window.scrollTo(0, 0);
		jQuery('#yt-off-resmenu').css('width','0px')		
		
		aa = jQuery( window ).width();
		if( ((aa*diff)/100) > leftSlide )
			aa=leftSlide;
		else
			aa=parseInt((aa*diff)/100);
		aa += 10;
		console.log(aa);

		jQuery('body').animate({left:aa},800);


		jQuery('body').addClass('body-position');		

		aa = jQuery( window ).width();
		if( ((aa*diff)/100) > leftSlide )
			aa=leftSlide;
		else
			aa=diff+'%';


		jQuery('#yt-off-resmenu').animate(
			{width:aa},
			800,
			function() {
				jQuery('#yt-off-resmenu').addClass('mm-opened');				
				jQuery('body').css({'overflow': 'hidden','height': '100%'});
				defaultOpen();								
		});

		jQuery('#yt-off-resmenu').addClass('mm-current');
		jQuery('#yt-off-resmenu').removeClass('mm-offcanvas');		

		return false;
	});				

	jQuery('.mm-subopen').click(function(){
		if('mm-0' == jQuery(this).parent().parent().attr('id') ){
			jQuery('.mm-list').each(function(){
				if('mm-0' == jQuery(this).attr('id') ){

				}else{
					jQuery(this).removeClass('mm-current');
					jQuery(this).removeClass('mm-subopened');
					jQuery(this).removeClass('mm-opened');	
					jQuery(this).removeClass('mm-highest');	
					jQuery(this).addClass('mm-hidden');
				}				
			})
		}

		

		currentUl = jQuery(this).attr('href');
		
		jQuery(currentUl).removeClass('mm-hidden');				
		jQuery(currentUl).addClass('mm-current');
		
		jQuery(currentUl).animate(
			{width:'100%'},
			100,
			function() {
				jQuery(currentUl).addClass('mm-opened');											
		});
		return false;
		
	})

	jQuery('.mm-subclose').click(function(){
		jQuery(this).parent().parent().removeClass('mm-current');				
		id = jQuery(this).parent().parent().attr('id');

		jQuery('#'+id).removeAttr("style");
		jQuery('#'+id).css('top',tops);
		jQuery('#'+id).removeClass('mm-opened');				
		currentUl = jQuery(this).attr('href');
		jQuery(currentUl).addClass('mm-current');			
		jQuery(currentUl).removeClass('mm-subopened');

		setTimeout(function() { jQuery('#'+id).addClass('mm-hidden'); }, 500);

		/*jQuery('#'+id).animate(
			{left:'700px'},
			700,
			,
			function(){															
				jQuery('#'+id).removeAttr("style");
				jQuery('#'+id).css('top',tops);
				jQuery('#'+id).removeClass('mm-opened');
				jQuery('#'+id).addClass('mm-hidden');
				currentUl = jQuery(this).attr('href');
				jQuery(currentUl).addClass('mm-current');			
				jQuery(currentUl).removeClass('mm-subopened');
			}
	);	*/			
		return false;
	})

	function setView(){

		//if(jQuery( window ).width() > 980){
		if(jQuery( window ).width() > 720){	
			if(jQuery('#yt-off-resmenu').hasClass('mm-offcanvas') == false){				
				jQuery('#mobile_menu_hide').click();
			}			
			jQuery('#mobile_menu_show').hide();
			jQuery('#rain_main_ul').show();
			
		}else{
			jQuery('#rain_main_ul').hide();
			jQuery('#mobile_menu_show').show();
		}

	}

		function defaultOpen(){

		fistTab = jQuery('#mm-0');
		
		jQuery('.mm-list').each(function(){		
			jQuery(this).removeClass('mm-current');
			jQuery(this).removeClass('mm-subopened');
			jQuery(this).removeClass('mm-opened');	
			jQuery(this).removeClass('mm-highest');	
			jQuery(this).addClass('mm-hidden');							
		})
				
		currentUl = fistTab;//jQuery(fistTab).attr('href');
		jQuery(currentUl).addClass('mm-current');	
		jQuery(currentUl).addClass('mm-opened');
		jQuery(currentUl).removeClass('mm-hidden');

		currentUl = jQuery('#mm-1');
		jQuery(currentUl).addClass('mm-current');	
		jQuery(currentUl).addClass('mm-opened');
		jQuery(currentUl).removeClass('mm-hidden');
				
		aa = jQuery( window ).width();
		if( ((aa*diff)/100) > leftSlide )
			aa=leftSlide;
		else
			aa=parseInt((aa*diff)/100);

		divWidth = jQuery('#yt-off-resmenu').width();
		totalWidth = 0;
		liHeight = 0;
		jQuery('#mm-0 li').each(function(){			
			totalWidth  = totalWidth+jQuery(this).width();
			liHeight = jQuery(this).height();
		});

		row = totalWidth/divWidth;
		row = parseInt(row)+1;
		tops = (row * liHeight)+40;		
		jQuery('.mm-menu > .mm-panel').css('top',tops+'px');
		
	}	

</script>
<style type="text/css">
:root{--cc-bg:#fff;--cc-text:#2d4156;--cc-btn-primary-bg:#2d4156;--cc-btn-primary-text:var(--cc-bg);--cc-btn-primary-hover-bg:#1d2e38;--cc-btn-secondary-bg:#eaeff2;--cc-btn-secondary-text:var(--cc-text);--cc-btn-secondary-hover-bg:#d8e0e6;--cc-toggle-bg-off:#919ea6;--cc-toggle-bg-on:var(--cc-btn-primary-bg);--cc-toggle-bg-readonly:#d5dee2;--cc-toggle-knob-bg:#fff;--cc-toggle-knob-icon-color:#ecf2fa;--cc-cookie-category-block-bg:#f0f4f7;--cc-cookie-category-block-bg-hover:#e9eff4;--cc-section-border:#f1f3f5;--cc-cookie-table-border:#e9edf2;--cc-overlay-bg:rgba(4, 6, 8, .6);--cc-webkit-scrollbar-bg:#cfd5db;--cc-webkit-scrollbar-bg-hover:#9199a0}.c_darkmode{--cc-bg:#181b1d;--cc-text:#d8e5ea;--cc-btn-primary-bg:#a6c4dd;--cc-btn-primary-text:#000;--cc-btn-primary-hover-bg:#c2dff7;--cc-btn-secondary-bg:#33383c;--cc-btn-secondary-text:var(--cc-text);--cc-btn-secondary-hover-bg:#3e454a;--cc-toggle-bg-off:#667481;--cc-toggle-bg-on:var(--cc-btn-primary-bg);--cc-toggle-bg-readonly:#454c54;--cc-toggle-knob-bg:var(--cc-cookie-category-block-bg);--cc-toggle-knob-icon-color:var(--cc-bg);--cc-cookie-category-block-bg:#23272a;--cc-cookie-category-block-bg-hover:#2b3035;--cc-section-border:#292d31;--cc-cookie-table-border:#2b3035;--cc-webkit-scrollbar-bg:#667481;--cc-webkit-scrollbar-bg-hover:#9199a0}.cc_div *,.cc_div :after,.cc_div :before{-webkit-box-sizing:border-box;box-sizing:border-box;float:none;font-style:inherit;font-variant:normal;font-weight:inherit;font-family:inherit;line-height:1.2;font-size:1em;transition:none;animation:none;margin:0;padding:0;text-transform:none;letter-spacing:unset;color:inherit;background:0 0;border:none;box-shadow:none;text-decoration:none;text-align:left;visibility:unset}.cc_div{font-size:16px;font-weight:400;font-family:-apple-system,sans-serif;color:#2d4156;color:var(--cc-text)}#c-ttl,#s-bl td:before,#s-ttl,.cc_div .b-tl,.cc_div .c-bn{font-weight:700}#cm,#s-bl .act .b-acc,#s-inr,.cc_div .b-tl,.cc_div .c-bl{border-radius:.25em}.cc_div a,.cc_div button,.cc_div input{-webkit-appearance:none;-moz-appearance:none;appearance:none}.cc_div a{text-decoration:underline}.cc_div a:hover{text-decoration:none}#cm-ov,#cs-ov,.c--anim #cm,.c--anim #s-cnt,.c--anim #s-inr{transition:visibility .25s ease,opacity .25s ease,transform .25s ease!important}.c--anim .c-bn{transition:background-color .25s ease!important}.c--anim #cm.bar.slide,.c--anim .bar.slide #s-inr{transition:visibility .4s ease,opacity .4s ease,transform .4s ease!important}.c--anim #cm.bar.slide+#cm-ov,.c--anim .bar.slide+#cs-ov{transition:visibility .4s ease,opacity .4s ease,transform .4s ease!important}#cm.bar.slide,.cc_div .bar.slide #s-inr{transform:translateX(100%);opacity:1}#cm.bar.top.slide,.cc_div .bar.left.slide #s-inr{transform:translateX(-100%);opacity:1}#cm.slide,.cc_div .slide #s-inr{transform:translateY(1.6em)}#cm.top.slide{transform:translateY(-1.6em)}#cm.bar.slide{transform:translateY(100%)}#cm.bar.top.slide{transform:translateY(-100%)}.show--consent .c--anim #cm,.show--consent .c--anim #cm.bar,.show--settings .c--anim #s-inr,.show--settings .c--anim .bar.slide #s-inr{opacity:1;transform:scale(1);visibility:visible!important}.show--settings .c--anim #s-cnt{visibility:visible!important}.force--consent.show--consent .c--anim #cm-ov,.show--settings .c--anim #cs-ov{visibility:visible!important;opacity:1!important}#cm{font-family:inherit;padding:1.2em 2.2em 1.825em 2.2em;position:fixed;z-index:1;background:#fff;background:var(--cc-bg);max-width:25em;width:100%;bottom:1.25em;right:1.25em;box-shadow:0 .625em 1.875em #000;box-shadow:0 .625em 1.875em rgba(2,2,3,.28);opacity:0;visibility:hidden;transform:scale(.95);line-height:initial}#c-ttl{margin:0 0 .6em 0;font-size:1.3em}#c-txt{margin-bottom:1.625em;font-size:.6em;line-height:1.45em}.cc_div .c-bn{color:#40505a;color:var(--cc-btn-secondary-text);background:#e5ebef;background:var(--cc-btn-secondary-bg);padding:1em 1.6em;display:inline-block;cursor:pointer;font-size:.85em;-moz-user-select:none;-khtml-user-select:none;-webkit-user-select:none;-o-user-select:none;user-select:none;text-align:center;border-radius:4px}#cm .c-bn{width:48.5%}#c-bns button+button,#s-c-bn,#s-cnt button+button{float:right}#cm .c_link:active,#cm .c_link:hover,#s-c-bn:active,#s-c-bn:hover,#s-cnt button+button:active,#s-cnt button+button:hover{background:#d8e0e6;background:var(--cc-btn-secondary-hover-bg)}#s-cnt{position:fixed;top:0;left:0;width:100%;z-index:101;display:table;height:100%;visibility:hidden}#s-bl{outline:0}#s-bl .title{margin-top:1.4em}#s-bl .title:first-child{margin-top:0}#s-bl .b-tl{font-size:1.1em}#s-bl .b-bn{margin-top:0}#s-bl .b-acc .p{margin-top:0;padding:1em}#s-cnt .b-bn .b-tl{display:block;font-family:inherit;font-size:1em;width:100%;cursor:pointer;position:relative;padding:1.4em 6.4em 1.4em 2.7em;background:0 0;transition:background-color .25s ease}#s-cnt .act .b-bn .b-tl{border-bottom-right-radius:0;border-bottom-left-radius:0}#s-cnt .b-bn .b-tl:active,#s-cnt .b-bn .b-tl:hover{background:#e9eff4;background:var(--cc-cookie-category-block-bg-hover)}#s-bl .b-bn{position:relative}#s-bl .c-bl{padding:1em;margin-bottom:.5em;border:1px solid #f1f3f5;border-color:var(--cc-section-border);transition:background-color .25s ease}#s-bl .c-bl:hover{background:#f0f4f7;background:var(--cc-cookie-category-block-bg)}#s-bl .c-bl:last-child{margin-bottom:.5em}#s-bl .c-bl:first-child{transition:none;padding:0;margin-top:0;border:none;margin-bottom:2em}#s-bl .c-bl:first-child:hover{background:0 0;background:unset}#s-bl .c-bl.b-ex{margin-top:2em;padding:0;border:none;background:#f0f4f7;background:var(--cc-cookie-category-block-bg);transition:none}#s-bl .c-bl.b-ex+.c-bl{margin-top:2em}#s-bl .c-bl.b-ex+.c-bl.b-ex{margin-top:0}#s-bl .c-bl.b-ex:first-child{margin-bottom:1em}#s-bl .c-bl.b-ex:first-child{margin-bottom:.5em}#s-bl .b-acc{max-height:0;overflow:hidden;padding-top:0;margin-bottom:0;display:none}#s-bl .act .b-acc{max-height:100%;display:block;overflow:hidden}#s-cnt .p{font-size:.9em;line-height:1.3em;margin-top:1em}.cc_div .c-tgl:disabled{cursor:not-allowed}#c-vln{display:table-cell;vertical-align:middle;position:relative}#cs{padding:0 1.7em;width:100%;position:fixed;left:0;right:0;top:0;bottom:0;height:100%}#s-inr{height:100%;position:relative;max-width:47em;margin:0 auto;transform:scale(.96);opacity:0;padding-top:5.125em;padding-bottom:4.9375em;position:relative;height:100%;overflow:hidden;visibility:hidden;box-shadow:rgba(3,6,9,.26) 0 13px 27px -5px}#s-bns,#s-hdr,#s-inr{background:#fff;background:var(--cc-bg)}#s-bl{overflow-y:auto;overflow-y:overlay;overflow-x:hidden;height:100%;padding:1.5em 2.5em;display:block;width:100%}#s-bns{position:absolute;bottom:0;left:0;right:0;padding:1em 2.5em;border-top:1px solid #f1f3f5;border-color:var(--cc-section-border);height:4.9375em}.cc_div .cc-link{color:#253b48;color:var(--cc-btn-primary-bg);border-bottom:1px solid #253b48;border-color:var(--cc-btn-primary-bg);display:inline;padding-bottom:0;text-decoration:none;cursor:pointer;font-weight:700}.cc_div .cc-link:active,.cc_div .cc-link:hover{border-color:transparent}#c-bns button:first-child,#s-bns button:first-child{color:#fff;color:var(--cc-btn-primary-text);background:#253b48;background:var(--cc-btn-primary-bg)}.cc_div .c-tgl:checked~.c-tg{background:#253b48;background:var(--cc-toggle-bg-on)}#c-bns button:first-child:active,#c-bns button:first-child:hover,#s-bns button:first-child:active,#s-bns button:first-child:hover{background:#1d2e38;background:var(--cc-btn-primary-hover-bg)}#s-hdr{position:absolute;top:0;width:100%;display:table;padding:1.2em 2.5em;vertical-align:middle;z-index:2;border-bottom:1px solid #f1f3f5;border-color:var(--cc-section-border)}#s-ttl{display:table-cell;vertical-align:middle;font-size:1em}#s-c-bn{padding:0;width:1.7em;height:1.7em;font-size:1.6em;margin:0;font-weight:initial;position:relative}#s-c-bnc{display:table-cell;vertical-align:middle}.cc_div span.t-lb{position:absolute;top:0;z-index:-1;opacity:0;pointer-events:none;overflow:hidden}#c_policy__text{height:31.25em;overflow-y:auto;margin-top:1.25em}#c-s-in{position:relative;transform:translateY(-50%);top:50%;height:100%;height:calc(100% - 2.5em);max-height:37.5em}#s-bl::-webkit-scrollbar{width:.9em;height:100%;background:0 0;border-radius:0 .25em .25em 0}#s-bl::-webkit-scrollbar-thumb{border:.25em solid var(--cc-bg);background:#cfd5db;background:var(--cc-webkit-scrollbar-bg);border-radius:100em}#s-bl::-webkit-scrollbar-thumb:hover{background:#9199a0;background:var(--cc-webkit-scrollbar-bg-hover)}#s-bl::-webkit-scrollbar-button{width:10px;height:5px}.cc_div .b-tg{position:absolute;right:0;top:0;bottom:0;display:inline-block;margin:auto;right:1.2em;cursor:pointer;-webkit-user-select:none;-moz-user-select:none;-ms-user-select:none;user-select:none;vertical-align:middle}.cc_div .c-tgl{position:absolute;cursor:pointer;display:block}.cc_div .b-tg .c-tg{position:absolute;overflow:hidden;background:#919ea6;background:var(--cc-toggle-bg-off);transition:background-color .25s ease;pointer-events:none}.cc_div .b-tg,.cc_div .b-tg .c-tg,.cc_div .c-tgl,.cc_div span.t-lb{width:3.6em;height:1.6em;border-radius:4em}.cc_div .b-tg .c-tg.c-ro{cursor:not-allowed}.cc_div .c-tgl~.c-tg.c-ro{background:#d5dee2;background:var(--cc-toggle-bg-readonly)}.cc_div .c-tgl~.c-tg.c-ro:after{box-shadow:none}.cc_div .b-tg .c-tg:after{content:"";position:absolute;left:.22em;top:.2em;width:1.2em;height:1.2em;border:none;box-sizing:content-box;background:#fff;background:var(--cc-toggle-knob-bg);box-shadow:0 1px 2px rgb(24 32 35 / 36%);transition:transform .25s ease;border-radius:100%}.cc_div .c-tgl:checked~.c-tg:after{transform:translateX(1.95em)}#s-bl table,#s-bl td,#s-bl th{border:none}#s-bl tbody tr{transition:background-color .25s ease}#s-bl tbody tr:hover{background:#e9eff4;background:var(--cc-cookie-category-block-bg-hover)}#s-bl table{text-align:left;border-collapse:collapse;width:100%;padding:0;margin:0;overflow:hidden}#s-bl td,#s-bl th{padding:.8em .625em;text-align:left;vertical-align:top;font-size:.8em;padding-left:1.2em}#s-bl th{font-family:inherit;padding:1.2em 1.2em}#s-bl thead tr:first-child{border-bottom:1px solid #e9edf2;border-color:var(--cc-cookie-table-border)}.force--consent #cs,.force--consent #s-cnt{width:100vw}#cm-ov,#cs-ov{position:fixed;left:0;right:0;top:0;bottom:0;visibility:hidden;opacity:0;background:#070707;background:rgba(4,6,8,.85);background:var(--cc-overlay-bg);display:none;transition:none}.c--anim #cs-ov,.force--consent .c--anim #cm-ov,.force--consent.show--consent #cm-ov,.show--settings #cs-ov{display:block}#cs-ov{z-index:2}.force--consent .cc_div{position:fixed;top:0;left:0;bottom:0;width:100%;width:100vw;visibility:hidden;transition:visibility .25s ease}.force--consent.show--consent .c--anim .cc_div,.force--consent.show--settings .c--anim .cc_div{visibility:visible}.force--consent #cm{position:absolute}.force--consent #cm.bar{width:100vw;max-width:100vw}html.force--consent.show--consent,html.force--consent.show--settings{overflow-y:hidden!important}html.force--consent,html.force--consent body{height:auto!important;overflow-x:hidden!important}.cc_div .act .b-bn .b-tl::before,.cc_div .b-bn .b-tl::before{border:solid #2d4156;border-color:var(--cc-btn-secondary-text);border-width:0 2px 2px 0;padding:.2em;display:inline-block;position:absolute;content:'';margin-right:15px;position:absolute;transform:translateY(-.2em) rotate(45deg);left:1.2em;top:1.85em}.cc_div .act .b-bn .b-tl::before{transform:translateY(.05em) rotate(225deg)}.cc_div .on-i::before{border:solid #fff;border-color:var(--cc-toggle-knob-icon-color);border-width:0 2px 2px 0;padding:.13em;display:inline-block;padding-bottom:.55em;content:'';margin:0 auto;transform:rotate(45deg);margin-top:.31em;margin-left:.1em}#s-c-bn::after,#s-c-bn::before{content:'';position:absolute;left:.82em;top:.55em;height:17px;width:1.5px;background:#444d53;background:var(--cc-btn-secondary-text);transform:rotate(45deg);border-radius:1em;margin:0 auto}#s-c-bn::after{transform:rotate(-45deg)}.cc_div .off-i,.cc_div .on-i{height:100%;width:50%;position:absolute;right:0;display:block;text-align:center;transition:opacity .25s ease}.cc_div .on-i{left:0;opacity:0}.cc_div .off-i::after,.cc_div .off-i::before{right:.84em;top:.4em;content:' ';height:.85em;width:.09375em;display:block;background:#cdd6dc;background:var(--cc-toggle-knob-icon-color);margin:0 auto;position:absolute;transform-origin:center}.cc_div .off-i::before{transform:rotate(45deg)}.cc_div .off-i::after{transform:rotate(-45deg)}.cc_div .c-tgl:checked~.c-tg .on-i{opacity:1}.cc_div .c-tgl:checked~.c-tg .off-i{opacity:0}#cm.cloud{max-width:50em;margin:0 auto;text-align:center;left:1.25em;right:1.25em;overflow:hidden;padding:1.3em 2.4em;width:unset}.cc_div .cloud #c-inr{display:table;width:100%}.cc_div .cloud #c-inr-i{width:70%;display:table-cell;vertical-align:top;padding-right:2.4em}.cc_div .cloud #c-ttl{font-size:1.1em}.cc_div .cloud #c-txt{margin-bottom:0;font-size:.85em}.cc_div .cloud #c-bns{min-width:170px;display:table-cell;vertical-align:middle}#cm.cloud .c-bn{margin:.625em 0 0 0;width:100%;font-size:.8em}#cm.cloud .c-bn:first-child{margin:0}#cm.cloud.left{margin-right:1.25em}#cm.cloud.right{margin-left:1.25em}#cm.bar{width:100%;max-width:100%;left:0;right:0;bottom:0;border-radius:0;position:fixed;padding:2em}#cm.bar #c-inr{max-width:32em;margin:0 auto}#cm.bar #c-bns{max-width:540px}#cm.bar #cs{padding:0}.cc_div .bar #c-s-in{top:0;transform:none;height:100%;max-height:100%}.cc_div .bar #s-bl,.cc_div .bar #s-bns,.cc_div .bar #s-hdr{padding-left:2em;padding-right:2em}.cc_div .bar #cs{padding:0}.cc_div .bar #s-inr{margin:0;margin-left:auto;margin-right:0;border-radius:0;max-width:32em}.cc_div .bar.left #s-inr{margin-left:0;margin-right:auto}.cc_div .bar #s-bl table,.cc_div .bar #s-bl tbody,.cc_div .bar #s-bl td,.cc_div .bar #s-bl th,.cc_div .bar #s-bl thead,.cc_div .bar #s-bl tr,.cc_div .bar #s-cnt{display:block}.cc_div .bar #s-bl thead tr{position:absolute;top:-9999px;left:-9999px}.cc_div .bar #s-bl tr{border-top:1px solid #e3e7ed;border-color:var(--cc-cookie-table-border)}.cc_div .bar #s-bl td{border:none;position:relative;padding-left:35%}.cc_div .bar #s-bl td:before{position:absolute;left:1em;padding-right:.625em;white-space:nowrap;content:attr(data-column);color:#000;color:var(--cc-text);overflow:hidden;text-overflow:ellipsis}#cm.top{bottom:auto;top:1.25em}#cm.left{right:auto;left:1.25em}#cm.right{left:auto;right:1.25em}#cm.bar.left,#cm.bar.right{left:0;right:0}#cm.bar.top{top:0}@media screen and (max-width:688px){#cm,#cm.cloud,#cm.left,#cm.right{width:100%;max-width:100%;margin:0;padding:1.875em;right:0;left:0;bottom:0;border-radius:0;display:block}.force--consent #cm,.force--consent #cm.cloud{width:100vw;max-width:100vw}#cm.top{top:0;bottom:unset}#cm.bottom{bottom:0;top:unset}.cc_div .cloud #c-ttl{font-size:1.3em}.cc_div .cloud #c-txt{font-size:.9em}#cm.cloud .c-bn{font-size:.85em}.cc_div .bar #s-inr{max-width:100%;width:100%}.cc_div .cloud #c-inr-i{padding-right:0}#cs{border-radius:0;padding:0}#c-s-in{max-height:100%;height:100%;top:0;transform:none}.cc_div .b-tg{font-size:1.25em;right:.9em}#s-inr{margin:0;padding-bottom:8.1em;border-radius:unset}#s-bl,.cc_div .bar #s-bl{padding:1.3em}#s-hdr,.cc_div .bar #s-hdr{padding:1.2em 1.3em}#s-bns,.cc_div .bar #s-bns{height:8.1em;padding:1em 1.3em}#s-bl table{width:100%}#s-bl table,#s-bl tbody,#s-bl td,#s-bl th,#s-bl thead,#s-bl tr,#s-cnt{display:block}#s-bl thead tr{position:absolute;top:-9999px;left:-9999px}#s-bl tr{border-top:1px solid #e3e7ed;border-color:var(--cc-cookie-table-border)}#s-bl td{border:none;position:relative;padding-left:35%}#s-bl td:before{position:absolute;left:1em;width:43%;padding-right:.625em;white-space:nowrap;content:attr(data-column);color:#000;color:var(--cc-text);overflow:hidden;text-overflow:ellipsis}#cm .c-bn,.cc_div .c-bn{width:100%;margin-right:0}#c-bns button+button,#s-cnt button+button{margin-top:.625em;float:unset}#cm.cloud{left:0;right:0;max-width:100%;width:100%}#cm.cloud.left,#cm.cloud.right{margin:0}.cc_div .cloud #c-bns,.cc_div .cloud #c-inr,.cc_div .cloud #c-inr-i{display:block;width:auto;min-width:auto}.cc_div .cloud #c-txt{margin-bottom:1.625em}}.cc_div.ie #c-vln{height:100%;padding-top:5.62em}.cc_div.ie .bar #c-vln{padding-top:0}.cc_div.ie #cs{max-height:37.5em;position:relative;top:0;margin-top:-5.625em}.cc_div.ie .bar #cs{margin-top:0;max-height:100%}.cc_div.ie #cm{border:1px solid #dee6e9}.cc_div.ie #c-s-in{top:0}.cc_div.ie .b-tg{padding-left:1em;margin-bottom:.7em}.cc_div.ie .c-tgl:checked~.c-tg:after{left:1.95em}.cc_div.ie #s-bl table{overflow:auto}.cc_div.ie .b-tg .c-tg{display:none}.cc_div.ie .c-tgl{position:relative;display:inline-block;vertical-align:middle;margin-bottom:.2em;height:auto}.cc_div.ie #s-cnt .b-bn .b-tl{padding:1.4em 6.4em 1.4em 1.4em}.cc_div.ie .bar #s-bl td:before{display:none}.cc_div.ie .bar #s-bl td{padding:.8em .625em .8em 1.2em}.cc_div.ie .bar #s-bl thead tr{position:relative}.cc_div.ie .b-tg .t-lb{filter: alpha(opacity=0);}.cc_div.ie #cm-ov,.cc_div.ie #cs-ov{filter: alpha(opacity=80);}

.table-row:nth-child(even) {background: #f5f5f5}
.table-row:nth-child(odd) {background: #e5e5e5}

.table-cell-1 {background: #f5f5f5; width:50px;
 	font-size: 2em;
	padding: 0;
	margin: 0;
	text-align: center;
	vertical-align: middle;
	border-radius: 8px;
	background-image: linear-gradient(0deg, #cdcdcd, #fff);
}
@media all and (max-width: 400px) {
.table-cell-1 {width:30px;
}
}

.table-cell-2 {
	width:100px;
 	font-size: 1em;
	padding: 0;
	margin: 0;
	text-align: center;
	vertical-align: middle;
	border-radius: 8px;
}
@media all and (max-width: 400px) {
.table-cell-2 {width:50px;
}
}

.table-cell-h {
	min-height:150px;
}
@media all and (max-width: 1100px) {
	.table-cell-h {
	 min-height: 130px; 
	}
}
@media all and (max-width: 800px) {
	.table-cell-h {
	 min-height: 110px; 
	}
}

.table-cell-3 {
	background: #ffffff; 
	padding: 0;
	margin: 0;
 	font-size: 1em;
	width:80%;
}

.table-cell-4 {
	width:20%;
 	font-size: 1em;
	padding: 0;
	margin: 0;
	text-align: left;
	vertical-align: middle;
}

.table-cell-5 {
	width:80%;
 	font-size: 1em;
	padding: 0;
	margin: 0;
	text-align: left;
	vertical-align: middle;
}
.table-cell {
	vertical-align: middle;
	padding:1%;
	font-size: clamp(0.6rem,1.5vw,1.4rem);
}
@media (min-width: 4em) {
.table { 
   display: table;
   border-spacing: 0.5em;
   width: 100%;
   margin:0;
   padding:0;
   border-spacing:0; 
   text-align: left;
}
.table-row {display: table-row; }
.table-cell {display: table-cell;}
.table-cell-1 {display: table-cell;}
.table-cell-2 {display: table-cell;}
.table-cell-3 {display: table-cell;}
.table-cell-4 {display: table-cell;}
.table-cell-5 {display: table-cell;}
.table-cell-6 {display: table-cell;}
.table-cell-7 {display: table-cell;}
.table-cell-8 {display: table-cell;}
.table-cell-9 {display: table-cell;}
.table-cell-10 {display: table-cell;}
.table-cell-11 {display: table-cell;}
.table-cell-12 {display: table-cell;}
.table-cell-13 {display: table-cell;}
.table-cell-14 {display: table-cell;}
}

.tableDiagram {table-layout:fixed;clear:both; width:100%;background-color:transparent;margin:0;padding:0;border-spacing:0;cellspacing:0;font-size: 1.2em;}
@media all and (max-width: 1100px) {
	.tableDiagram {
	 font-size: 1.0em; 
	}
}
@media all and (max-width: 800px) {
	.tableDiagram {
	 font-size: 0.8em; 
	}
}
.Eingabefeld {
	width: 100%;
	font-size: 1.4em;
}
@media all and (max-width: 400px) {
.Eingabefeld {
	font-size: 1em;
}
}
.Suchfeld {
	float:right; width: 30%;
}
@media all and (max-width: 1200px) {
.Suchfeld {
	width: 50%;
}
}
@media all and (max-width: 600px) {
.Suchfeld {
	width: 80%;
}
}
#MasterMitte {
	font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
	height: 100%;
	width: auto;
	margin-left: 5%;
	margin-right: clamp(250px, 15%, 300px);
	padding: 0;
	overflow: hidden; 
	background-color: white;
	font-size: clamp(0.8rem, 2.5vw, 1.1rem); 
}
@media all and (max-width: 800px) {
	#MasterMitte {
	margin-left: auto;
	margin-right: auto;
 	 width: 90%;
	}
}
@media all and (max-width: 400px) {
	#MasterMitte {
	margin-left: auto;
	margin-right: auto;
 	 width: 96%;
	}
}
p {
	font-size: 1em;
	margin: 0;
	padding: 0;
	padding-top: 5px;
}
.box-2 {
	clear:both;
	text-align: justify;
	width: 98%;
	margin: 0;
	margin-top: 2%;
	padding: 1%;
}
.box-2-h {
	float:left;
	text-align: justify;
	width: 45%;
	margin: 0;
	margin-top: 2%;
	padding: 1%;
}
@media all and (max-width: 600px) {
.box-2-h {
	width: 98%;
}
}
.box-3 {
	clear:both;
	text-align: justify;
	width: 98%;
	margin: 0;
	margin-top: 2%;
	padding: 1%;
}
.box-3 a {line-height: 3.5;}
.box-3 a:visited { color: #AA3939; font-weight: normal;}
.box-3 a:active { color: #AA3939; font-weight: normal;}
.box-3 a:link { color: blue; font-weight: normal;}
.box-3 a:hover { color: white; background-color: #004C66; font-weight: normal;}

.LinkListe {
 margin-left: 15px;
}
@media all and (max-width: 600px) {
	.LinkListe {
		margin-left:30px;
	}
}
img {
	display:block;
	margin-left: auto;
	margin-right: auto;
	width:80%;
}
.FormelBoxC {
 clear: both;
 font-size: clamp(1.0rem,2vw,1.8rem); 
 text-align: center; 
 margin-top: 10px; 
 margin-bottom: 10px;
}
.FormelBoxCLi {
 font-family:Latin-modern;
 font-style:italic;
 text-align: center; 
 font-size: clamp(1.0rem,2vw,1.8rem);
}
.FormelBoxLi {
 font-family:Latin-modern;
 font-style:italic;
 text-align: left; 
 font-size: clamp(1.0rem,2vw,1.8rem);
}
.FormelBoxL {
 clear: both;
 font-size: clamp(1.0rem,2vw,1.8rem); 
 text-align: left; 
 margin-top: 10px; 
 margin-bottom: 10px;
}
  footer#fuss {
	clear:both;
	width:98%;
	margin: 10px;
	padding: 0;
	box-shadow: 5px 5px 10px grey;
  }
  footer#fuss p {
  	font-family:Bookman;
	text-align:center;
	margin: 0;
	padding: 0;
    padding-bottom: 15px; padding-top: 15px;
  }
footer#fuss p a:link {color:black; font-weight:bold; text-decoration:none; padding-left: 5px; padding-right: 5px}
footer#fuss p a:visited {color:black; font-weight:bold; text-decoration:none; padding-left: 5px; padding-right: 5px}
footer#fuss p a:hover {color:red; font-weight:bold; text-decoration:none; padding-left: 5px; padding-right: 5px}
footer#fuss p a:active {color:black; font-weight:bold; text-decoration:none; padding-left: 5px; padding-right: 5px}
@media all and (max-width: 800px) {
	footer#fuss {
	 font-size: 0.8em; 
 	 width:90%;
	}
}
.tRechner {
 margin:0;
 padding:0;
 width: 100%;
 border-spacing: 5px;
 font-size: 0.8em;
 background-color: transparent;
 empty-cells:hide;
}
@media all and (max-width: 800px) {
	.tRechner {
	 font-size: 1.2em;
	 }
}
@media all and (max-width: 700px) {
	.tRechner {
	 font-size: 1.0em;
	 }
}
@media all and (max-width: 600px) {
	.tRechner {
	 font-size: 0.8em;
	 }
}
.tRechner td {
    padding: 0;
	text-align: center;
	vertical-align: middle;
	border-radius: 8px;
	height: 2em;
	background-image: linear-gradient(0deg, #cdcdcd, #fff);
}
.tRechner td:hover { background-image: linear-gradient(0deg, #fff, #cdcdcd);}
.matrixK {
margin: 5px;
padding: 8px;
border-left: 3px solid black;
border-right: 3px solid black;
border-top: 0px solid black;
border-bottom: 0px solid black;
border-bottom-left-radius: 30px; 
border-bottom-right-radius: 30px; 
border-top-left-radius: 30px; 
border-top-right-radius: 30px;
}
@media all and (max-width: 1100px) {
	.matrixK {
	border-left: 2px solid black;
	border-right: 2px solid black;
	}
}
@media all and (max-width: 800px) {
	.matrixK {
	border-left: 1px solid black;
	border-right: 1px solid black;
	}
}
.werbung-unten {
	clear:both;
    padding-top: 30px;
}
.selection {margin-top:10px;}
/* Chrome, Safari and Opera syntax */
:-webkit-full-screen {
  background-color: white;
}
/* Firefox syntax */
:-moz-full-screen {
  background-color: white;
}
/* IE/Edge syntax */
:-ms-fullscreen {
  background-color: white;
}
/* Standard syntax */
:fullscreen {
  background-color: white;
}
.grid-rechner {
  width: 100%;
  display: grid;
  grid-template-columns: repeat(9, 1fr); 
  grid-auto-rows: auto;
  grid-gap: 8px;
  background-color: #f5f5f5;
  padding: 2px;
  border-radius: 5px; 
  align-items: center;
  max-width:500px;
  float:left;
  font-weight:500;
}
.grid-rechner > div {
  text-align: center;
  padding: 4px;
  min-height: 25px;
  font-size: clamp(0.7rem,1.2vw,1.0rem);
  border-radius: 5px; 
}
.grid-funktionen {
  display: grid;
  grid-template-columns: repeat(10, 1fr); 
  grid-auto-rows: 1fr;
  grid-gap: 1vw;
  background-color: #f5f5f5;
  padding: 1vw;
  border-radius: 1vw; 
}
.grid-funktionen > div {
  text-align: left;
  padding: 0.6vw;
  font-size: clamp(0.7rem,1.2vw,1.0rem);
  border-radius: 1vw; 
}
.itemfkt1 {
  grid-column: span 10;
  align-self: center;
}
.itemfkt2 {
  grid-column: span 2;
  align-self: center;
}
.itemfkt3 {
  grid-column: span 8;
  align-self: center;
}
span.frac {
	display: inline-block;
	text-align: center;
}
span.frac > sup {
	display: block;
	border-bottom: 1px solid;
	font: inherit;
}
span.frac > span {
	display: none;
}
span.frac > sub {
	display: block;
	font: inherit;
}
.itemBlank {
  grid-column: span 1;
}
.itemcl {
  background-image: linear-gradient(0deg, #cdcdcd, #fff);
  grid-column: span 2;
  color:red;
}
.itemcl:hover {
  background-image: linear-gradient(0deg, #fff, #555);
}
.itemok {
  background-image: linear-gradient(0deg, #cdcdcd, #fff);
  grid-column: span 2;
  color:green;
}
.itemok:hover {
  background-image: linear-gradient(0deg, #fff, #555);
}
.item1 {
  background-image: linear-gradient(0deg, #cdcdcd, #fff);
  grid-column: span 1;
}
.item1:hover {
  background-image: linear-gradient(0deg, #fff, #555);
}
.item2 {
  background-image: linear-gradient(0deg, #cdcdcd, #fff);
  grid-column: span 2;
}
.item2:hover {
  background-image: linear-gradient(0deg, #fff, #555);
}
.item3 {
  background-image: linear-gradient(0deg, #cdcdcd, #fff);
  grid-column: span 3;
}
.item3:hover {
  background-image: linear-gradient(0deg, #fff, #555);
}
.txtArea {
 border:3px solid grey;
 width:95%;
 font-size: clamp(0.7rem,1.4vw,2.0rem);
}
h1 {
  font-size: clamp(1.0rem,3vw,2.5rem);
  text-align: left;
}
h2 {
  font-size: clamp(0.9rem,2.6vw,2.4rem);
  text-align: left;
  clear: both;
}
h3 {
  font-size: clamp(0.8rem,2.4vw,2.3rem);
  text-align: left;
  clear: both;
}
h4 {
  font-size: clamp(0.8rem,2.1vw,2.3rem);
  text-align: left;
  font-weight: normal;
}
.cImg {width:40%;float:right;}
@media all and (max-width: 600px) {
	.cImg {width:100%;}
}
.fktList {float:right;margin:0;padding:0;width:35%;font-size: clamp(0.8rem,1.1vw,1.3rem)}
@media all and (max-width: 1150px) {
	.fktList {width:100%;}
}
.select {
  padding: 0px;
  margin: 8px;
  border-radius: 5px;
  font-size: clamp(0.6rem,1.7vw,1rem);
  cursor: pointer;
}
.Eingabe {
  text-align: center; 
  font-size: clamp(0.6rem,1.7vw,1rem);
  width: clamp(4em,7vw,8em);
  border-radius: 5px;
  margin: 8px;
  cursor: pointer;
}
.EingabeS {
  text-align: center; 
  font-size: clamp(0.6rem,1.7vw,1rem);
  width: clamp(3.5em,3vw,4em);
  border-radius: 5px;
  margin: 8px;
  cursor: pointer;
}
.cButton {
  background-image: linear-gradient(0deg, #cdcdcd, #fff);
  padding:0px;
  margin:8px;
  border-radius: 5px;
  border: 2px solid #cdcdcd;
  font-size: clamp(0.6rem,1.7vw,1.2rem);
  width: clamp(2em,8vw,4em);
  height: clamp(2.5em,2vw,2.8em);
  cursor: pointer;
}
.cButton:hover { color: blue; text-decoration:none; border: 2px solid blue;background-image: linear-gradient(0deg, #fff, #555);}
.cButton:active { color: red; cursor: wait; text-decoration:none; border: 2px solid blue;background-image: linear-gradient(0deg, #fff, #555);}
.cButtonL {
  background-image: linear-gradient(0deg, #cdcdcd, #fff);
  padding:2px;
  margin:8px;
  border-radius: 5px;
  border: 2px solid #cdcdcd;
  font-size: clamp(0.6rem,1.7vw,1.2rem);
  min-height: clamp(2.8em,2vw,3em);
  cursor: pointer;
}
.cButtonL:hover { color: blue; text-decoration:none; border: 2px solid blue;background-image: linear-gradient(0deg, #fff, #555);}
.cButtonL:active { color: red; cursor: wait; text-decoration:none; border: 2px solid blue;background-image: linear-gradient(0deg, #fff, #555);}

</style>
</head>
<body onload="drawDiagramm1();" onresize="Resize();">
<div style="visibility: hidden; overflow: hidden; position: absolute; top: 0px; height: 1px; width: auto; padding: 0px; border: 0px; margin: 0px; text-align: left; text-indent: 0px; text-transform: none; line-height: normal; letter-spacing: normal; word-spacing: normal;">
<div id="MathJax_Hidden">
</div>
</div>

<div id="MathJax_Message" style="display: none;" _msttexthash="465855" _msthash="392"></div>
	<div id="MasterMitte" style="height: auto !important;">
		<div class="Suchfeld">
		<div class="gcse-searchbox-only">
		</div>
		</div>
		<div class="box-2" style="height: auto !important;">
		
			<div class="table">
				<div class="table-row">
					<div class="table-cell" title="The ratio of length and height of the grafic. 1:1 means a square grafic.">
						<span style="padding:5px;margin:5px;" _msttexthash="766038" _msthash="6">⃢</span>
					</div>
					<div class="table-cell"><font _mstmutation="1" _msttexthash="815217" _msthash="13">
						↹#.000</font><input onfocus="this.select()" type="number" id="digits" value="3" onchange="digitfkt()" class="EingabeS">
					</div>
					<div class="table-cell" title="Zoom factor."><font _mstmutation="1" _msttexthash="11928475" _msthash="14">
					</font><input onfocus="this.select()" type="number" id="zoom-x" value="1.2" min="1" max="5" step="0.2" onchange="Resize()" class="EingabeS">
					</div>
					<div class="table-cell" title="Zoom factor."><font _mstmutation="1" _msttexthash="11928592" _msthash="15">
					</font><input onfocus="this.select()" type="number" id="zoom-y" value="1.2" min="1" max="5" step="0.2" onchange="Resize()" class="EingabeS">
					</div>
					<div class="table-cell" title="Screenshot: The function copys the grafic to a jpg-format. So the grafic is storable.">
						<input type="button" value="⎙" onclick="Screenshot()" title="Screenshot" class="cButton" _mstvalue="829283" _msthash="16">
					</div>
					<div class="table-cell" title="Fullscreen: Switch to fullscreen format. Return with esc.">
						<input type="button" value="⛶" onclick="openFullscreen()" title="FullScreen" class="cButton" _mstvalue="907634" _msthash="17">
					</div>
				</div>
			</div>
			</div>
			<div id="jxgboxPoly" class="jxgbox" style="height: 973px; user-select: none; overflow: hidden; position: relative; touch-action: none;">
			<svg width="1946" height="973" style="overflow: hidden; width: 1946px; height: 973px;"><defs><filter id="jxgboxPoly_f1" width="300%" height="300%" filterUnits="userSpaceOnUse"><feoffset result="offOut" in="SourceAlpha" dx="5" dy="5"></feoffset><fegaussianblur result="blurOut" in="offOut" stdDeviation="3"></fegaussianblur><feblend in="SourceGraphic" in2="blurOut" mode="normal"></feblend></filter><marker id="jxgboxPoly_jxgBoard1L3TriangleStart" stroke="#666666" stroke-opacity="1" fill="#666666" fill-opacity="1" stroke-width="0" orient="auto" markerUnits="strokeWidth" refY="5" refX="0.1" display="inherit" viewBox="0 0 80 80" markerHeight="64" markerWidth="64" style="position: absolute;"><path d="M 0,0 L 10,5 L 0,10 z"></path></marker><marker id="jxgboxPoly_jxgBoard1L18TriangleStart" stroke="#666666" stroke-opacity="1" fill="#666666" fill-opacity="1" stroke-width="0" orient="auto" markerUnits="strokeWidth" refY="5" refX="0.1" display="inherit" viewBox="0 0 80 80" markerHeight="64" markerWidth="64" style="position: absolute;"><path d="M 0,0 L 10,5 L 0,10 z"></path></marker></defs><g><ellipse id="jxgboxPoly_jxgBoard1P1" style="position: absolute; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: hidden;" stroke="#0000ff" stroke-opacity="1" stroke-width="2px" fill="red" fill-opacity="1" cx="124" cy="872" rx="4" ry="4" display="none"></ellipse><ellipse id="jxgboxPoly_jxgBoard1P2" style="position: absolute; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: hidden;" stroke="#0000ff" stroke-opacity="1" stroke-width="2px" fill="red" fill-opacity="1" cx="278" cy="872" rx="4" ry="4" display="none"></ellipse><ellipse id="jxgboxPoly_jxgBoard1P16" style="position: absolute; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: hidden;" stroke="#0000ff" stroke-opacity="1" stroke-width="2px" fill="red" fill-opacity="1" cx="124" cy="872" rx="4" ry="4" display="none"></ellipse><ellipse id="jxgboxPoly_jxgBoard1P17" style="position: absolute; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: hidden;" stroke="#0000ff" stroke-opacity="1" stroke-width="2px" fill="red" fill-opacity="1" cx="124" cy="517" rx="4" ry="4" display="none"></ellipse></g><g></g><g><line id="jxgboxPoly_jxgBoard1L3" style="position: absolute; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: inherit;" stroke="#666666" stroke-opacity="1" stroke-width="1px" fill-opacity="0" x1="4" y1="871.5484199796126" x2="1933.9999999999995" y2="871.5484199796126" marker-end="url(#jxgboxPoly_jxgBoard1L3TriangleStart)" stroke-linecap="butt" display="inline"></line><path id="jxgboxPoly_jxgBoard1L3_ticks_1" stroke-linecap="round" stroke-linejoin="round" stroke="#666666" fill="none" stroke-opacity="0.25" stroke-width="1" d=" M 154 872 L 154 872 L 154 877 M 185 872 L 185 872 L 185 877 M 216 872 L 216 872 L 216 877 M 247 872 L 247 872 L 247 877 M 278 0 L 278 973 M 309 872 L 309 872 L 309 877 M 340 872 L 340 872 L 340 877 M 371 872 L 371 872 L 371 877 M 402 872 L 402 872 L 402 877 M 432 0 L 432 973 M 463 872 L 463 872 L 463 877 M 494 872 L 494 872 L 494 877 M 525 872 L 525 872 L 525 877 M 556 872 L 556 872 L 556 877 M 587 0 L 587 973 M 618 872 L 618 872 L 618 877 M 649 872 L 649 872 L 649 877 M 680 872 L 680 872 L 680 877 M 710 872 L 710 872 L 710 877 M 741 0 L 741 973 M 772 872 L 772 872 L 772 877 M 803 872 L 803 872 L 803 877 M 834 872 L 834 872 L 834 877 M 865 872 L 865 872 L 865 877 M 896 0 L 896 973 M 927 872 L 927 872 L 927 877 M 958 872 L 958 872 L 958 877 M 988 872 L 988 872 L 988 877 M 1019 872 L 1019 872 L 1019 877 M 1050 0 L 1050 973 M 1081 872 L 1081 872 L 1081 877 M 1112 872 L 1112 872 L 1112 877 M 1143 872 L 1143 872 L 1143 877 M 1174 872 L 1174 872 L 1174 877 M 1205 0 L 1205 973 M 1236 872 L 1236 872 L 1236 877 M 1266 872 L 1266 872 L 1266 877 M 1297 872 L 1297 872 L 1297 877 M 1328 872 L 1328 872 L 1328 877 M 1359 0 L 1359 973 M 1390 872 L 1390 872 L 1390 877 M 1421 872 L 1421 872 L 1421 877 M 1452 872 L 1452 872 L 1452 877 M 1483 872 L 1483 872 L 1483 877 M 1514 0 L 1514 973 M 1544 872 L 1544 872 L 1544 877 M 1575 872 L 1575 872 L 1575 877 M 1606 872 L 1606 872 L 1606 877 M 1637 872 L 1637 872 L 1637 877 M 1668 0 L 1668 973 M 1699 872 L 1699 872 L 1699 877 M 1730 872 L 1730 872 L 1730 877 M 1761 872 L 1761 872 L 1761 877 M 1792 872 L 1792 872 L 1792 877 M 1822 0 L 1822 973 M 1853 872 L 1853 872 L 1853 877 M 1884 872 L 1884 872 L 1884 877 M 1915 872 L 1915 872 L 1915 877 M 93 872 L 93 872 L 93 877 M 62 872 L 62 872 L 62 877 M 31 872 L 31 872 L 31 877 M 0 872 L 0 872 L 0 877" display="inline" style="position: absolute; visibility: inherit;"></path><line id="jxgboxPoly_jxgBoard1L18" style="position: absolute; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: inherit;" stroke="#666666" stroke-opacity="1" stroke-width="1px" fill-opacity="0" x1="123.55555555555554" y1="969" x2="123.55555555555554" y2="12" marker-end="url(#jxgboxPoly_jxgBoard1L18TriangleStart)" stroke-linecap="butt" display="inline"></line><path id="jxgboxPoly_jxgBoard1L18_ticks_1" stroke-linecap="round" stroke-linejoin="round" stroke="#666666" fill="none" stroke-opacity="0.25" stroke-width="1" d=" M 119 836 L 124 836 L 124 836 M 119 801 L 124 801 L 124 801 M 119 765 L 124 765 L 124 765 M 119 730 L 124 730 L 124 730 M 0 694 L 1946 694 M 119 659 L 124 659 L 124 659 M 119 624 L 124 624 L 124 624 M 119 588 L 124 588 L 124 588 M 119 553 L 124 553 L 124 553 M 0 517 L 1946 517 M 119 482 L 124 482 L 124 482 M 119 446 L 124 446 L 124 446 M 119 411 L 124 411 L 124 411 M 119 376 L 124 376 L 124 376 M 0 340 L 1946 340 M 119 305 L 124 305 L 124 305 M 119 269 L 124 269 L 124 269 M 119 234 L 124 234 L 124 234 M 119 199 L 124 199 L 124 199 M 0 163 L 1946 163 M 119 128 L 124 128 L 124 128 M 119 92 L 124 92 L 124 92 M 119 57 L 124 57 L 124 57 M 119 21 L 124 21 L 124 21 M 119 907 L 124 907 L 124 907 M 119 942 L 124 942 L 124 942" display="inline" style="position: absolute; visibility: inherit;"></path></g><g></g><g></g><g><path id="jxgboxPoly_jxgBoard1G44" stroke-linecap="round" stroke-linejoin="round" style="position: absolute; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: inherit;" stroke="red" stroke-opacity="1" stroke-width="2px" fill-opacity="0" d=" M 0 369.0462237049392 L 0.9501953124999858 369.1222498964704 L 1.900390625 369.19827608800153 L 2.8505859375 369.2743022795327 L 3.80078125 369.3503284710638 L 4.750976562499986 369.4263546625949 L 5.701171874999986 369.50238085412605 L 6.651367187499986 369.57840704565723 L 7.601562499999986 369.65443323718836 L 8.5517578125 369.73045942871954 L 9.501953124999986 369.8064856202506 L 10.452148437499986 369.88251181178174 L 11.402343749999972 369.9585380033129 L 12.352539062499972 370.03456419484405 L 13.302734374999986 370.1105903863752 L 14.252929687499986 370.18661657790636 L 15.203124999999986 370.26264276943743 L 16.15332031249997 370.33866896096856 L 17.103515624999986 370.41469515249975 L 18.0537109375 370.4907213440309 L 19.003906249999986 370.566747535562 L 19.954101562499986 370.6427737270932 L 20.904296875 370.71879991862426 L 21.8544921875 370.7948261101554 L 22.8046875 370.87085230168657 L 23.754882812499986 370.9468784932177 L 24.705078125 371.0229046847488 L 25.655273437500014 371.09893087628 L 26.60546875 371.1749570678111 L 27.5556640625 371.2509832593422 L 28.505859374999986 371.3270094508734 L 29.456054687499986 371.4030356424045 L 30.40625 371.47906183393565 L 31.3564453125 371.55508802546683 L 32.306640625 371.6311142169979 L 33.256835937499986 371.707140408529 L 34.207031249999986 371.7831666000602 L 35.15722656249997 371.85919279159134 L 36.107421874999986 371.93521898312247 L 37.0576171875 372.01124517465365 L 38.007812499999986 372.0872713661847 L 38.958007812499986 372.16329755771585 L 39.908203124999986 372.23932374924703 L 40.8583984375 372.31534994077816 L 41.80859375 372.3913761323093 L 42.758789062499986 372.46740232384036 L 43.708984375 372.54342851537155 L 44.659179687500014 372.6194547069027 L 45.609375 372.69548089843386 L 46.5595703125 372.771507089965 L 47.509765625 372.8475332814961 L 48.4599609375 372.9235594730272 L 49.41015625 372.99958566455837 L 50.3603515625 373.0756118560895 L 51.310546875 373.1516380476207 L 52.2607421875 373.2276642391518 L 53.2109375 373.30369043068293 L 54.1611328125 373.379716622214 L 55.111328125 373.4557428137452 L 56.0615234375 373.5317690052763 L 57.01171875 373.6077951968075 L 57.9619140625 373.68382138833863 L 58.912109374999986 373.75984757986976 L 59.86230468749999 373.8358737714009 L 60.81249999999999 373.911899962932 L 61.76269531249999 373.98792615446314 L 62.712890625 374.0639523459943 L 63.66308593749999 374.13997853752545 L 64.61328125 374.21600472905664 L 65.5634765625 374.2920309205877 L 66.51367187499999 374.36805711211883 L 67.46386718749999 374.44408330364996 L 68.4140625 374.52010949518115 L 69.3642578125 374.5961356867123 L 70.314453125 374.67216187824346 L 71.2646484375 374.7481880697745 L 72.21484375 374.82421426130566 L 73.1650390625 374.9002404528368 L 74.115234375 374.97626664436797 L 75.0654296875 375.0522928358991 L 76.015625 375.1283190274303 L 76.9658203125 375.20434521896135 L 77.91601562499999 375.2803714104925 L 78.8662109375 375.3563976020236 L 79.81640625 375.4324237935548 L 80.7666015625 375.5084499850859 L 81.716796875 375.5844761766171 L 82.66699218749999 375.6605023681482 L 83.6171875 375.7365285596793 L 84.5673828125 375.8125547512104 L 85.51757812499999 375.8885809427416 L 86.46777343749999 375.96460713427274 L 87.41796874999999 376.0406333258039 L 88.36816406249999 376.116659517335 L 89.318359375 376.1926857088661 L 90.2685546875 376.26871190039725 L 91.21875 376.34473809192843 L 92.16894531249999 376.42076428345956 L 93.11914062499999 376.49679047499075 L 94.06933593749999 376.5728166665218 L 95.01953125 376.64884285805294 L 95.9697265625 376.7248690495841 L 96.91992187499999 376.80089524111526 L 97.87011718749999 376.8769214326464 L 98.82031249999999 376.95294762417757 L 99.7705078125 377.02897381570864 L 100.72070312499999 377.10500000723977 L 101.67089843749999 377.1810261987709 L 102.62109374999999 377.2570523903021 L 103.57128906249999 377.3330785818332 L 104.52148437499999 377.4091047733644 L 105.47167968749999 377.48513096489546 L 106.42187499999999 377.5611571564266 L 107.37207031249999 377.6371833479577 L 108.32226562499999 377.7132095394889 L 109.27246093749999 377.78923573102 L 110.22265624999999 377.8652619225512 L 111.17285156249999 377.9412881140823 L 112.12304687499999 378.0173143056134 L 113.07324218749999 378.0933404971446 L 114.02343749999999 378.1693666886757 L 114.97363281249999 378.24539288020685 L 115.92382812499999 378.32141907173803 L 116.87402343749999 378.3974452632691 L 117.82421874999999 378.47347145480023 L 118.77441406249999 378.5494976463314 L 119.72460937499999 378.62552383786254 L 120.67480468749999 378.7015500293937 L 121.62499999999999 378.77757622092474 L 122.57519531249999 378.8536024124559 L 123.52539062499999 378.92962860398706 L 124.47558593749999 379.00565479551824 L 125.42578124999999 379.08168098704937 L 126.37597656249999 379.1577071785805 L 127.32617187499999 379.23373337011157 L 128.27636718749997 379.30975956164275 L 129.22656249999997 379.3857857531739 L 130.1767578125 379.46181194470506 L 131.12695312499997 379.5378381362362 L 132.07714843749997 379.6138643277673 L 133.02734374999997 379.6898905192984 L 133.97753906249997 379.7659167108296 L 134.92773437499997 379.8419429023607 L 135.87792968749997 379.9179690938919 L 136.82812499999997 379.993995285423 L 137.77832031249997 380.07002147695414 L 138.728515625 380.1460476684852 L 139.6787109375 380.2220738600164 L 140.62890624999997 380.2981000515475 L 141.57910156249997 380.3741262430787 L 142.52929687499997 380.45015243460983 L 143.47949218749997 380.52617862614096 L 144.42968749999997 380.60220481767203 L 145.37988281249997 380.6782310092032 L 146.33007812499997 380.75425720073434 L 147.28027343749997 380.8302833922655 L 148.23046874999997 380.90630958379666 L 149.18066406249997 380.9823357753278 L 150.13085937499997 381.05836196685885 L 151.0810546875 381.13438815839004 L 152.03124999999997 381.21041434992117 L 152.98144531249997 381.28644054145235 L 153.93164062499997 381.3624667329835 L 154.88183593749997 381.4384929245146 L 155.83203125 381.5145191160457 L 156.7822265625 381.59054530757686 L 157.732421875 381.666571499108 L 158.68261718749997 381.7425976906392 L 159.63281249999997 381.8186238821703 L 160.5830078125 381.8946500737014 L 161.53320312499997 381.97067626523256 L 162.48339843749997 382.0467024567637 L 163.43359374999997 382.1227286482948 L 164.38378906249997 382.198754839826 L 165.333984375 382.2747810313571 L 166.28417968749997 382.3508072228883 L 167.23437499999997 382.4268334144194 L 168.18457031249997 382.5028596059505 L 169.13476562499997 382.57888579748163 L 170.08496093749997 382.6549119890128 L 171.03515624999997 382.73093818054394 L 171.98535156249997 382.80696437207513 L 172.93554687499997 382.8829905636062 L 173.88574218749997 382.9590167551373 L 174.83593749999997 383.03504294666845 L 175.7861328125 383.11106913819964 L 176.736328125 383.18709532973077 L 177.68652343749997 383.26312152126195 L 178.63671874999997 383.339147712793 L 179.58691406249997 383.41517390432415 L 180.53710937499997 383.4912000958553 L 181.48730468749997 383.56722628738646 L 182.43749999999997 383.6432524789176 L 183.38769531249997 383.7192786704488 L 184.33789062499997 383.79530486197984 L 185.28808593749997 383.87133105351097 L 186.23828124999997 383.9473572450421 L 187.18847656249997 384.0233834365733 L 188.13867187499997 384.0994096281044 L 189.08886718749997 384.1754358196356 L 190.03906249999997 384.25146201116667 L 190.98925781249997 384.3274882026978 L 191.93945312499997 384.4035143942289 L 192.88964843749997 384.4795405857601 L 193.83984375 384.55556677729123 L 194.7900390625 384.6315929688224 L 195.740234375 384.7076191603535 L 196.69042968749997 384.7836453518846 L 197.64062499999997 384.85967154341574 L 198.5908203125 384.9356977349469 L 199.54101562499997 385.01172392647806 L 200.49121093749997 385.0877501180091 L 201.44140624999997 385.1637763095403 L 202.3916015625 385.23980250107144 L 203.341796875 385.31582869260257 L 204.29199218749997 385.39185488413375 L 205.2421875 385.4678810756649 L 206.1923828125 385.54390726719606 L 207.142578125 385.61993345872713 L 208.0927734375 385.69595965025826 L 209.04296874999997 385.7719858417894 L 209.99316406249997 385.8480120333206 L 210.94335937499997 385.9240382248517 L 211.8935546875 386.00006441638277 L 212.84374999999997 386.07609060791395 L 213.79394531249997 386.1521167994451 L 214.744140625 386.22814299097627 L 215.6943359375 386.3041691825074 L 216.64453125 386.3801953740385 L 217.59472656249997 386.4562215655696 L 218.54492187499997 386.5322477571008 L 219.49511718749994 386.6082739486319 L 220.44531249999997 386.6843001401631 L 221.3955078125 386.7603263316942 L 222.34570312499997 386.83635252322534 L 223.29589843749997 386.9123787147564 L 224.24609374999994 386.9884049062876 L 225.19628906249994 387.0644310978187 L 226.14648437499997 387.1404572893499 L 227.09667968749997 387.21648348088104 L 228.04687499999997 387.29250967241217 L 228.99707031249994 387.36853586394324 L 229.94726562499997 387.4445620554744 L 230.8974609375 387.52058824700555 L 231.84765624999997 387.59661443853673 L 232.79785156249997 387.67264063006786 L 233.748046875 387.748666821599 L 234.6982421875 387.82469301313006 L 235.6484375 387.90071920466124 L 236.59863281249997 387.97674539619237 L 237.548828125 388.05277158772356 L 238.4990234375 388.1287977792547 L 239.44921875 388.2048239707858 L 240.3994140625 388.2808501623169 L 241.34960937499997 388.35687635384807 L 242.29980468749997 388.4329025453792 L 243.24999999999997 388.5089287369104 L 244.2001953125 388.5849549284415 L 245.150390625 388.66098111997263 L 246.10058593749997 388.7370073115037 L 247.05078124999997 388.8130335030349 L 248.00097656249994 388.889059694566 L 248.95117187499997 388.9650858860972 L 249.9013671875 389.0411120776283 L 250.85156249999997 389.11713826915945 L 251.80175781249997 389.1931644606905 L 252.75195312499997 389.2691906522217 L 253.7021484375 389.34521684375284 L 254.65234374999997 389.421243035284 L 255.60253906249997 389.49726922681515 L 256.552734375 389.5732954183463 L 257.5029296875 389.64932160987735 L 258.453125 389.72534780140853 L 259.4033203125 389.80137399293966 L 260.353515625 389.87740018447084 L 261.3037109375 389.95342637600197 L 262.25390625 390.0294525675331 L 263.2041015625 390.10547875906417 L 264.154296875 390.18150495059535 L 265.1044921875 390.2575311421265 L 266.0546875 390.33355733365767 L 267.0048828125 390.4095835251888 L 267.955078125 390.48560971672 L 268.9052734375 390.56163590825105 L 269.85546875 390.6376620997822 L 270.8056640625 390.7136882913133 L 271.755859375 390.7897144828445 L 272.7060546875 390.8657406743756 L 273.65625 390.9417668659068 L 274.6064453125 391.01779305743787 L 275.556640625 391.093819248969 L 276.5068359375 391.1698454405001 L 277.45703125 391.2458716320313 L 278.4072265625 391.32189782356244 L 279.357421875 391.3979240150936 L 280.3076171875 391.4739502066247 L 281.2578125 391.5499763981558 L 282.20800781249994 391.62600258968695 L 283.15820312499994 391.70202878121813 L 284.1083984375 391.77805497274926 L 285.05859375 391.85408116428044 L 286.00878906249994 391.9301073558115 L 286.958984375 392.00613354734264 L 287.9091796875 392.08215973887377 L 288.859375 392.15818593040495 L 289.8095703125 392.2342121219361 L 290.75976562499994 392.31023831346715 L 291.7099609375 392.38626450499834 L 292.66015625 392.46229069652946 L 293.6103515625 392.5383168880606 L 294.560546875 392.6143430795918 L 295.5107421875 392.6903692711229 L 296.4609375 392.7663954626541 L 297.4111328125 392.84242165418516 L 298.361328125 392.9184478457163 L 299.3115234375 392.9944740372474 L 300.26171874999994 393.0705002287786 L 301.21191406249994 393.1465264203097 L 302.16210937499994 393.2225526118408 L 303.1123046875 393.298578803372 L 304.0625 393.3746049949031 L 305.01269531249994 393.45063118643424 L 305.962890625 393.5266573779654 L 306.9130859375 393.60268356949655 L 307.86328125 393.6787097610276 L 308.8134765625 393.7547359525588 L 309.76367187499994 393.83076214408993 L 310.71386718749994 393.90678833562106 L 311.66406249999994 393.98281452715224 L 312.61425781249994 394.05884071868337 L 313.5644531249999 394.13486691021444 L 314.51464843749994 394.2108931017456 L 315.46484374999994 394.28691929327675 L 316.41503906249994 394.3629454848079 L 317.365234375 394.43897167633907 L 318.3154296875 394.5149978678702 L 319.26562499999994 394.59102405940126 L 320.21582031249994 394.66705025093245 L 321.16601562499994 394.7430764424636 L 322.1162109375 394.81910263399476 L 323.06640625 394.8951288255259 L 324.01660156249994 394.971155017057 L 324.966796875 395.0471812085881 L 325.9169921875 395.12320740011927 L 326.8671875 395.1992335916504 L 327.8173828125 395.2752597831816 L 328.76757812499994 395.3512859747127 L 329.7177734375 395.42731216624384 L 330.66796875 395.5033383577749 L 331.6181640625 395.5793645493061 L 332.568359375 395.6553907408372 L 333.5185546875 395.7314169323684 L 334.46875 395.80744312389953 L 335.4189453125 395.88346931543066 L 336.369140625 395.95949550696173 L 337.3193359375 396.0355216984929 L 338.26953125 396.11154789002404 L 339.2197265625 396.1875740815552 L 340.169921875 396.26360027308635 L 341.1201171875 396.3396264646175 L 342.0703125 396.41565265614855 L 343.0205078125 396.49167884767974 L 343.970703125 396.56770503921086 L 344.9208984375 396.64373123074205 L 345.87109375 396.7197574222732 L 346.8212890625 396.7957836138043 L 347.77148437499994 396.8718098053354 L 348.7216796875 396.94783599686656 L 349.671875 397.0238621883977 L 350.6220703125 397.09988837992887 L 351.572265625 397.17591457146 L 352.5224609375 397.2519407629911 L 353.47265625 397.3279669545222 L 354.4228515625 397.4039931460534 L 355.373046875 397.4800193375845 L 356.32324218749994 397.5560455291157 L 357.27343749999994 397.6320717206468 L 358.22363281249994 397.7080979121779 L 359.17382812499994 397.784124103709 L 360.1240234375 397.8601502952402 L 361.07421874999994 397.93617648677133 L 362.02441406249994 398.0122026783025 L 362.974609375 398.08822886983364 L 363.9248046875 398.16425506136477 L 364.875 398.24028125289584 L 365.82519531249994 398.316307444427 L 366.77539062499994 398.39233363595815 L 367.7255859375 398.46835982748934 L 368.67578125 398.54438601902046 L 369.6259765625 398.62041221055154 L 370.576171875 398.6964384020827 L 371.5263671875 398.77246459361385 L 372.4765625 398.848490785145 L 373.4267578125 398.92451697667616 L 374.376953125 399.0005431682073 L 375.32714843749994 399.07656935973847 L 376.27734374999994 399.15259555126954 L 377.22753906249994 399.22862174280067 L 378.17773437499994 399.3046479343318 L 379.1279296875 399.380674125863 L 380.07812499999994 399.4567003173941 L 381.02832031249994 399.5327265089252 L 381.978515625 399.60875270045636 L 382.92871093749994 399.6847788919875 L 383.87890624999994 399.7608050835186 L 384.82910156249994 399.8368312750498 L 385.77929687499994 399.91285746658093 L 386.72949218749994 399.988883658112 L 387.67968749999994 400.0649098496432 L 388.62988281249994 400.1409360411743 L 389.58007812499994 400.21696223270544 L 390.53027343749994 400.2929884242366 L 391.48046874999994 400.36901461576775 L 392.43066406249994 400.4450408072988 L 393.38085937499994 400.52106699883 L 394.33105468749994 400.59709319036114 L 395.28124999999994 400.67311938189226 L 396.23144531249994 400.74914557342345 L 397.18164062499994 400.8251717649546 L 398.13183593749994 400.90119795648565 L 399.08203124999994 400.97722414801683 L 400.03222656249994 401.05325033954796 L 400.982421875 401.1292765310791 L 401.93261718749994 401.20530272261027 L 402.88281249999994 401.2813289141414 L 403.83300781249994 401.35735510567247 L 404.78320312499994 401.43338129720365 L 405.7333984375 401.5094074887348 L 406.68359374999994 401.5854336802659 L 407.63378906249994 401.6614598717971 L 408.583984375 401.7374860633282 L 409.5341796875 401.8135122548593 L 410.484375 401.8895384463905 L 411.43457031249994 401.9655646379216 L 412.38476562499994 402.04159082945273 L 413.3349609375 402.1176170209839 L 414.28515625 402.19364321251504 L 415.23535156249994 402.2696694040461 L 416.185546875 402.3456955955773 L 417.1357421875 402.4217217871084 L 418.0859375 402.49774797863955 L 419.0361328125 402.57377417017074 L 419.98632812499994 402.64980036170186 L 420.93652343749994 402.72582655323293 L 421.88671874999994 402.8018527447641 L 422.83691406249994 402.87787893629525 L 423.78710937499994 402.95390512782643 L 424.73730468749994 403.02993131935756 L 425.68749999999994 403.1059575108887 L 426.63769531249994 403.18198370241976 L 427.587890625 403.25800989395094 L 428.5380859375 403.33403608548207 L 429.48828124999994 403.41006227701325 L 430.43847656249994 403.4860884685444 L 431.38867187499994 403.5621146600755 L 432.33886718749994 403.6381408516066 L 433.28906249999994 403.71416704313776 L 434.2392578124999 403.7901932346689 L 435.18945312499994 403.8662194262001 L 436.13964843749994 403.9422456177312 L 437.08984375 404.01827180926233 L 438.0400390625 404.0942980007934 L 438.99023437499994 404.1703241923246 L 439.94042968749994 404.2463503838557 L 440.89062499999994 404.3223765753869 L 441.8408203125 404.398402766918 L 442.79101562499994 404.47442895844915 L 443.7412109374999 404.5504551499802 L 444.69140624999994 404.6264813415114 L 445.64160156249994 404.70250753304254 L 446.591796875 404.7785337245737 L 447.5419921875 404.85455991610485 L 448.49218749999994 404.930586107636 L 449.44238281249994 405.00661229916705 L 450.39257812499994 405.08263849069823 L 451.3427734375 405.15866468222936 L 452.29296875 405.23469087376054 L 453.24316406250006 405.31071706529167 L 454.193359375 405.3867432568228 L 455.14355468749994 405.46276944835387 L 456.09375 405.53879563988505 L 457.0439453125 405.6148218314162 L 457.99414062499994 405.69084802294736 L 458.94433593749994 405.7668742144785 L 459.89453124999994 405.84290040600956 L 460.8447265625 405.9189265975407 L 461.794921875 405.9949527890719 L 462.74511718750006 406.070978980603 L 463.6953125 406.1470051721342 L 464.64550781249994 406.2230313636653 L 465.595703125 406.29905755519644 L 466.5458984375 406.3750837467275 L 467.49609375000006 406.4511099382587 L 468.44628906250006 406.5271361297898 L 469.396484375 406.603162321321 L 470.3466796875 406.67918851285214 L 471.296875 406.75521470438326 L 472.24707031250006 406.8312408959144 L 473.197265625 406.9072670874455 L 474.14746093749994 406.98329327897665 L 475.09765625 407.05931947050783 L 476.0478515625 407.13534566203896 L 476.99804687499994 407.21137185357014 L 477.94824218749994 407.2873980451012 L 478.89843749999994 407.36342423663234 L 479.8486328125 407.43945042816347 L 480.79882812499994 407.51547661969465 L 481.7490234374999 407.5915028112258 L 482.69921874999994 407.66752900275685 L 483.64941406249994 407.74355519428804 L 484.599609375 407.81958138581916 L 485.5498046875 407.8956075773503 L 486.49999999999994 407.9716337688815 L 487.45019531249994 408.0476599604126 L 488.40039062499994 408.1236861519437 L 489.3505859375 408.19971234347486 L 490.30078125 408.275738535006 L 491.25097656250006 408.3517647265371 L 492.201171875 408.4277909180683 L 493.15136718749994 408.5038171095994 L 494.1015625 408.5798433011305 L 495.0517578125 408.6558694926617 L 496.00195312499994 408.7318956841928 L 496.95214843749994 408.80792187572393 L 497.90234374999994 408.8839480672551 L 498.8525390625 408.95997425878625 L 499.80273437499994 409.0360004503173 L 500.7529296874999 409.1120266418485 L 501.70312499999994 409.18805283337963 L 502.65332031249994 409.26407902491076 L 503.6035156249999 409.34010521644194 L 504.5537109374999 409.416131407973 L 505.5039062499999 409.49215759950414 L 506.45410156249994 409.5681837910353 L 507.40429687499994 409.64420998256645 L 508.3544921875 409.7202361740976 L 509.30468749999994 409.79626236562876 L 510.2548828124999 409.8722885571599 L 511.20507812499994 409.94831474869096 L 512.1552734375 410.02434094022215 L 513.10546875 410.1003671317533 L 514.0556640625 410.1763933232844 L 515.005859375 410.2524195148156 L 515.9560546875 410.32844570634666 L 516.90625 410.4044718978778 L 517.8564453125 410.48049808940897 L 518.806640625 410.5565242809401 L 519.7568359374999 410.6325504724712 L 520.70703125 410.7085766640024 L 521.6572265625 410.78460285553354 L 522.607421875 410.8606290470646 L 523.5576171875 410.9366552385958 L 524.5078125 411.0126814301269 L 525.4580078125 411.0887076216581 L 526.408203125 411.16473381318923 L 527.3583984375 411.24076000472036 L 528.30859375 411.3167861962514 L 529.2587890625 411.3928123877826 L 530.208984375 411.46883857931374 L 531.1591796875 411.5448647708449 L 532.109375 411.62089096237605 L 533.0595703125 411.6969171539072 L 534.009765625 411.77294334543825 L 534.9599609375 411.84896953696943 L 535.91015625 411.92499572850056 L 536.8603515625 412.00102192003175 L 537.810546875 412.0770481115629 L 538.7607421875 412.153074303094 L 539.7109375 412.2291004946251 L 540.6611328125 412.30512668615626 L 541.611328125 412.3811528776874 L 542.5615234375 412.45717906921857 L 543.51171875 412.5332052607497 L 544.4619140625 412.6092314522808 L 545.412109375 412.6852576438119 L 546.3623046875 412.7612838353431 L 547.3125 412.8373100268742 L 548.2626953125 412.9133362184054 L 549.212890625 412.9893624099365 L 550.1630859375 413.0653886014676 L 551.11328125 413.1414147929987 L 552.0634765625 413.2174409845299 L 553.013671875 413.29346717606103 L 553.9638671875 413.3694933675922 L 554.9140625 413.44551955912334 L 555.8642578125 413.52154575065447 L 556.814453125 413.59757194218554 L 557.7646484375 413.6735981337167 L 558.71484375 413.74962432524785 L 559.6650390625 413.82565051677904 L 560.615234375 413.90167670831016 L 561.5654296875 413.97770289984123 L 562.515625 414.05372909137236 L 563.4658203125 414.12975528290355 L 564.416015625 414.2057814744347 L 565.3662109375 414.28180766596586 L 566.31640625 414.357833857497 L 567.2666015625 414.4338600490281 L 568.216796875 414.5098862405592 L 569.1669921875 414.58591243209037 L 570.1171875 414.6619386236215 L 571.0673828125 414.7379648151527 L 572.017578125 414.8139910066838 L 572.9677734374999 414.8900171982149 L 573.91796875 414.96604338974606 L 574.8681640625 415.0420695812772 L 575.818359375 415.1180957728083 L 576.7685546875 415.1941219643395 L 577.71875 415.27014815587063 L 578.6689453125 415.3461743474017 L 579.619140625 415.4222005389329 L 580.5693359375 415.498226730464 L 581.51953125 415.57425292199514 L 582.4697265625 415.6502791135263 L 583.419921875 415.72630530505745 L 584.3701171875 415.8023314965885 L 585.3203125 415.8783576881197 L 586.2705078125 415.95438387965083 L 587.220703125 416.03041007118196 L 588.1708984375 416.10643626271315 L 589.12109375 416.1824624542443 L 590.0712890625 416.25848864577534 L 591.021484375 416.33451483730653 L 591.9716796874999 416.41054102883766 L 592.921875 416.4865672203688 L 593.8720703125 416.56259341189997 L 594.822265625 416.6386196034311 L 595.7724609374999 416.71464579496217 L 596.7226562499999 416.79067198649335 L 597.6728515625 416.8666981780245 L 598.623046875 416.9427243695556 L 599.5732421875 417.0187505610868 L 600.5234375 417.0947767526179 L 601.4736328124999 417.170802944149 L 602.423828125 417.2468291356802 L 603.3740234375 417.3228553272113 L 604.32421875 417.3988815187424 L 605.2744140625 417.4749077102736 L 606.224609375 417.55093390180474 L 607.1748046875 417.6269600933358 L 608.125 417.702986284867 L 609.0751953125 417.7790124763981 L 610.025390625 417.85503866792925 L 610.9755859374999 417.93106485946043 L 611.92578125 418.00709105099156 L 612.8759765625 418.08311724252263 L 613.826171875 418.1591434340538 L 614.7763671875 418.23516962558494 L 615.7265625 418.3111958171161 L 616.6767578125 418.38722200864726 L 617.626953125 418.4632482001784 L 618.5771484375 418.53927439170945 L 619.52734375 418.61530058324064 L 620.4775390625 418.69132677477177 L 621.427734375 418.7673529663029 L 622.3779296875 418.8433791578341 L 623.328125 418.9194053493652 L 624.2783203125 418.9954315408963 L 625.228515625 419.07145773242746 L 626.1787109375 419.1474839239586 L 627.12890625 419.2235101154898 L 628.0791015625 419.2995363070209 L 629.029296875 419.375562498552 L 629.9794921874999 419.4515886900831 L 630.9296875 419.5276148816143 L 631.8798828125 419.6036410731454 L 632.830078125 419.6796672646766 L 633.7802734374999 419.7556934562077 L 634.7304687499999 419.8317196477388 L 635.6806640624999 419.9077458392699 L 636.630859375 419.9837720308011 L 637.5810546875 420.05979822233223 L 638.53125 420.1358244138634 L 639.4814453124999 420.21185060539455 L 640.4316406249999 420.2878767969256 L 641.3818359375 420.36390298845674 L 642.33203125 420.4399291799879 L 643.2822265625 420.51595537151906 L 644.232421875 420.59198156305024 L 645.1826171874999 420.66800775458137 L 646.1328125 420.7440339461125 L 647.0830078125 420.82006013764357 L 648.033203125 420.89608632917475 L 648.9833984374999 420.9721125207059 L 649.9335937499999 421.04813871223706 L 650.8837890625 421.1241649037682 L 651.8339843749999 421.20019109529926 L 652.7841796874999 421.2762172868304 L 653.7343749999999 421.3522434783616 L 654.6845703124999 421.4282696698927 L 655.6347656249999 421.5042958614239 L 656.5849609374999 421.580322052955 L 657.5351562499999 421.6563482444861 L 658.4853515624999 421.7323744360172 L 659.4355468749999 421.8084006275484 L 660.3857421875 421.8844268190795 L 661.3359374999999 421.9604530106107 L 662.2861328124999 422.03647920214183 L 663.2363281249999 422.1125053936729 L 664.1865234374999 422.18853158520403 L 665.13671875 422.2645577767352 L 666.0869140625 422.34058396826634 L 667.037109375 422.41661015979753 L 667.9873046874999 422.49263635132866 L 668.9374999999999 422.5686625428597 L 669.8876953125 422.64468873439085 L 670.8378906249999 422.72071492592204 L 671.7880859374999 422.79674111745317 L 672.7382812499999 422.87276730898435 L 673.6884765624999 422.9487935005155 L 674.638671875 423.02481969204655 L 675.5888671875 423.10084588357773 L 676.5390625 423.17687207510886 L 677.4892578124999 423.25289826664 L 678.4394531249999 423.3289244581712 L 679.3896484375 423.4049506497023 L 680.33984375 423.4809768412335 L 681.2900390625 423.55700303276456 L 682.240234375 423.6330292242957 L 683.1904296874999 423.7090554158268 L 684.140625 423.785081607358 L 685.0908203125 423.8611077988891 L 686.041015625 423.9371339904202 L 686.9912109374999 424.0131601819514 L 687.9414062499999 424.0891863734825 L 688.8916015625 424.16521256501363 L 689.8417968749999 424.2412387565448 L 690.7919921874999 424.31726494807594 L 691.7421874999999 424.393291139607 L 692.6923828124999 424.4693173311382 L 693.6425781249999 424.5453435226693 L 694.5927734374999 424.62136971420045 L 695.5429687499999 424.69739590573164 L 696.4931640624999 424.7734220972627 L 697.4433593749999 424.84944828879384 L 698.3935546875 424.925474480325 L 699.3437499999999 425.00150067185615 L 700.2939453124999 425.0775268633873 L 701.2441406249999 425.15355305491846 L 702.1943359374999 425.2295792464496 L 703.14453125 425.30560543798066 L 704.0947265625 425.38163162951184 L 705.0449218749999 425.457657821043 L 705.9951171874999 425.5336840125741 L 706.9453124999999 425.6097102041053 L 707.8955078125 425.68573639563635 L 708.8457031249999 425.7617625871675 L 709.7958984374999 425.83778877869867 L 710.7460937499999 425.9138149702298 L 711.6962890624999 425.9898411617609 L 712.6464843749999 426.0658673532921 L 713.5966796874999 426.1418935448232 L 714.5468749999999 426.2179197363543 L 715.4970703124999 426.2939459278855 L 716.4472656249999 426.3699721194166 L 717.3974609374998 426.44599831094774 L 718.3476562499999 426.5220245024789 L 719.2978515624999 426.59805069401 L 720.2480468749999 426.6740768855411 L 721.1982421874999 426.7501030770723 L 722.1484374999999 426.82612926860344 L 723.0986328124999 426.90215546013457 L 724.0488281249999 426.97818165166575 L 724.9990234374999 427.0542078431969 L 725.9492187499999 427.13023403472795 L 726.8994140625 427.20626022625913 L 727.8496093749999 427.28228641779026 L 728.7998046874999 427.35831260932144 L 729.7499999999999 427.4343388008526 L 730.7001953124999 427.51036499238364 L 731.6503906249999 427.58639118391477 L 732.6005859374999 427.66241737544595 L 733.5507812499999 427.7384435669771 L 734.5009765624999 427.81446975850827 L 735.4511718749999 427.8904959500394 L 736.4013671875 427.9665221415705 L 737.3515624999999 428.0425483331016 L 738.3017578124999 428.1185745246328 L 739.2519531249999 428.1946007161639 L 740.2021484374999 428.2706269076951 L 741.15234375 428.3466530992262 L 742.1025390625 428.4226792907573 L 743.0527343749999 428.4987054822884 L 744.0029296874999 428.5747316738196 L 744.9531249999999 428.6507578653507 L 745.9033203125 428.7267840568819 L 746.853515625 428.80281024841304 L 747.8037109374999 428.8788364399441 L 748.7539062499999 428.95486263147524 L 749.7041015624999 429.0308888230064 L 750.6542968749998 429.10691501453755 L 751.6044921874999 429.18294120606873 L 752.5546874999999 429.2589673975998 L 753.5048828124999 429.33499358913093 L 754.4550781249999 429.41101978066206 L 755.4052734374998 429.48704597219324 L 756.3554687499999 429.56307216372437 L 757.3056640624999 429.63909835525556 L 758.2558593749998 429.7151245467866 L 759.2060546874998 429.79115073831775 L 760.1562499999998 429.8671769298489 L 761.1064453124999 429.94320312138007 L 762.0566406249999 430.0192293129112 L 763.0068359374998 430.0952555044424 L 763.9570312499998 430.17128169597345 L 764.9072265624998 430.2473078875046 L 765.8574218749997 430.3233340790357 L 766.8076171874998 430.3993602705669 L 767.7578124999998 430.475386462098 L 768.7080078124998 430.5514126536292 L 769.6582031249998 430.6274388451603 L 770.6083984374999 430.7034650366914 L 771.5585937499999 430.7794912282225 L 772.5087890624999 430.8555174197537 L 773.4589843749999 430.93154361128484 L 774.4091796874998 431.007569802816 L 775.3593749999999 431.0835959943471 L 776.3095703124999 431.1596221858782 L 777.2597656249998 431.2356483774094 L 778.2099609374998 431.31167456894053 L 779.1601562499998 431.38770076047166 L 780.1103515624999 431.46372695200284 L 781.0605468749999 431.53975314353397 L 782.0107421874999 431.61577933506504 L 782.9609374999999 431.6918055265962 L 783.9111328125 431.76783171812735 L 784.861328125 431.8438579096585 L 785.8115234374999 431.91988410118967 L 786.7617187499999 431.99591029272074 L 787.7119140624999 432.07193648425186 L 788.6621093749998 432.14796267578305 L 789.6123046874999 432.2239888673142 L 790.5624999999999 432.3000150588453 L 791.5126953124999 432.3760412503765 L 792.4628906249999 432.4520674419076 L 793.4130859374998 432.5280936334387 L 794.3632812499999 432.60411982496987 L 795.3134765624999 432.680146016501 L 796.2636718749998 432.7561722080321 L 797.2138671874998 432.8321983995632 L 798.1640624999998 432.9082245910944 L 799.1142578124999 432.9842507826255 L 800.0644531249999 433.0602769741567 L 801.0146484374999 433.1363031656878 L 801.9648437499999 433.21232935721895 L 802.9150390625 433.28835554875013 L 803.865234375 433.36438174028126 L 804.8154296874999 433.44040793181233 L 805.7656249999999 433.5164341233435 L 806.7158203124999 433.59246031487464 L 807.6660156249998 433.66848650640577 L 808.6162109374999 433.74451269793684 L 809.5664062499999 433.820538889468 L 810.5166015624999 433.89656508099915 L 811.4667968749999 433.97259127253034 L 812.4169921875 434.04861746406146 L 813.3671875 434.1246436555926 L 814.3173828125 434.2006698471238 L 815.267578125 434.2766960386549 L 816.2177734374999 434.352722230186 L 817.16796875 434.42874842171716 L 818.1181640625 434.5047746132483 L 819.0683593749999 434.5808008047794 L 820.0185546874999 434.6568269963106 L 820.9687499999999 434.73285318784167 L 821.9189453125 434.8088793793728 L 822.869140625 434.884905570904 L 823.8193359374999 434.9609317624351 L 824.7695312499999 435.03695795396624 L 825.7197265624999 435.1129841454974 L 826.6699218749998 435.1890103370285 L 827.6201171874999 435.2650365285596 L 828.5703124999999 435.3410627200908 L 829.5205078124999 435.41708891162193 L 830.4707031249999 435.4931151031531 L 831.4208984374999 435.56914129468424 L 832.37109375 435.6451674862153 L 833.3212890625 435.72119367774644 L 834.271484375 435.7972198692776 L 835.2216796874999 435.87324606080875 L 836.1718749999999 435.94927225233994 L 837.1220703125 436.02529844387107 L 838.0722656249999 436.10132463540214 L 839.0224609374999 436.17735082693326 L 839.9726562499999 436.25337701846445 L 840.9228515624999 436.3294032099956 L 841.873046875 436.40542940152676 L 842.8232421875 436.4814555930579 L 843.7734375 436.55748178458896 L 844.7236328125 436.6335079761201 L 845.6738281250001 436.70953416765127 L 846.6240234375 436.7855603591824 L 847.57421875 436.8615865507136 L 848.5244140625 436.9376127422447 L 849.4746093749999 437.0136389337758 L 850.4248046874999 437.0896651253069 L 851.375 437.1656913168381 L 852.3251953125 437.2417175083692 L 853.275390625 437.3177436999004 L 854.2255859374999 437.3937698914315 L 855.1757812499999 437.4697960829626 L 856.1259765625 437.54582227449373 L 857.0761718749999 437.6218484660249 L 858.0263671874999 437.69787465755604 L 858.9765624999999 437.7739008490872 L 859.9267578124999 437.84992704061835 L 860.876953125 437.9259532321494 L 861.8271484375 438.00197942368055 L 862.77734375 438.07800561521174 L 863.7275390625 438.15403180674286 L 864.6777343750001 438.23005799827405 L 865.6279296875 438.3060841898052 L 866.578125 438.38211038133625 L 867.5283203125 438.4581365728674 L 868.4785156249999 438.53416276439856 L 869.4287109374999 438.6101889559297 L 870.37890625 438.68621514746087 L 871.3291015625 438.762241338992 L 872.279296875 438.8382675305231 L 873.2294921875 438.9142937220542 L 874.1796875000001 438.9903199135854 L 875.1298828125001 439.0663461051165 L 876.0800781250001 439.1423722966477 L 877.0302734375 439.2183984881788 L 877.98046875 439.2944246797099 L 878.9306640625001 439.3704508712411 L 879.880859375 439.4464770627722 L 880.8310546875 439.52250325430333 L 881.78125 439.5985294458345 L 882.7314453125 439.67455563736564 L 883.6816406250001 439.7505818288968 L 884.6318359375 439.8266080204279 L 885.58203125 439.902634211959 L 886.5322265625 439.97866040349015 L 887.4824218749999 440.05468659502134 L 888.4326171874999 440.1307127865524 L 889.3828125 440.20673897808354 L 890.3330078125 440.2827651696147 L 891.283203125 440.35879136114585 L 892.2333984374999 440.434817552677 L 893.1835937499999 440.51084374420816 L 894.1337890625 440.5868699357393 L 895.0839843749999 440.66289612727036 L 896.0341796874999 440.73892231880154 L 896.9843749999999 440.81494851033267 L 897.9345703124999 440.8909747018638 L 898.884765625 440.967000893395 L 899.8349609374999 441.04302708492605 L 900.7851562499999 441.1190532764572 L 901.7353515624999 441.19507946798836 L 902.6855468749998 441.2711056595195 L 903.6357421874998 441.3471318510506 L 904.5859374999999 441.4231580425818 L 905.5361328124999 441.4991842341129 L 906.4863281249999 441.575210425644 L 907.4365234374999 441.6512366171752 L 908.38671875 441.7272628087063 L 909.3369140625 441.80328900023744 L 910.287109375 441.8793151917686 L 911.2373046874999 441.9553413832997 L 912.1874999999999 442.0313675748308 L 913.1376953125 442.107393766362 L 914.0878906249999 442.18341995789314 L 915.0380859374999 442.25944614942426 L 915.9882812499999 442.33547234095545 L 916.9384765624999 442.4114985324866 L 917.888671875 442.48752472401765 L 918.8388671875 442.56355091554883 L 919.7890625 442.63957710707996 L 920.7392578125 442.7156032986111 L 921.6894531250001 442.79162949014227 L 922.6396484375 442.86765568167334 L 923.58984375 442.94368187320447 L 924.5400390625 443.01970806473565 L 925.4902343749999 443.0957342562668 L 926.4404296874999 443.1717604477979 L 927.390625 443.2477866393291 L 928.3408203125 443.3238128308602 L 929.291015625 443.3998390223913 L 930.2412109374999 443.4758652139225 L 931.1914062499999 443.5518914054536 L 932.1416015625 443.6279175969848 L 933.0917968749999 443.70394378851586 L 934.0419921874999 443.779969980047 L 934.9921874999999 443.8559961715781 L 935.9423828124999 443.9320223631093 L 936.892578125 444.0080485546404 L 937.8427734374999 444.0840747461716 L 938.7929687499999 444.16010093770274 L 939.7431640624999 444.2361271292338 L 940.6933593749998 444.31215332076493 L 941.6435546874998 444.3881795122961 L 942.5937499999999 444.46420570382725 L 943.5439453124999 444.54023189535843 L 944.4941406249999 444.6162580868895 L 945.4443359374998 444.69228427842063 L 946.3945312499998 444.76831046995176 L 947.3447265624999 444.84433666148294 L 948.2949218749998 444.92036285301407 L 949.2451171874998 444.99638904454525 L 950.1953124999998 445.0724152360763 L 951.1455078124998 445.14844142760745 L 952.0957031249999 445.2244676191386 L 953.0458984374999 445.30049381066976 L 953.9960937499999 445.3765200022009 L 954.9462890624999 445.4525461937321 L 955.896484375 445.5285723852632 L 956.8466796874999 445.6045985767943 L 957.7968749999999 445.6806247683254 L 958.7470703124999 445.7566509598566 L 959.6972656249998 445.8326771513877 L 960.6474609374998 445.9087033429189 L 961.5976562499999 445.98472953445 L 962.5478515624999 446.0607557259811 L 963.4980468749999 446.1367819175122 L 964.4482421874999 446.2128081090434 L 965.3984375 446.28883430057454 L 966.3486328125 446.3648604921057 L 967.298828125 446.44088668363685 L 968.2490234374999 446.5169128751679 L 969.1992187499999 446.59293906669905 L 970.1494140625 446.66896525823023 L 971.0996093749999 446.74499144976136 L 972.0498046874999 446.82101764129254 L 972.9999999999999 446.89704383282367 L 973.9501953124999 446.97307002435474 L 974.900390625 447.04909621588587 L 975.8505859374999 447.12512240741705 L 976.8007812499999 447.2011485989482 L 977.7509765624999 447.27717479047936 L 978.7011718749998 447.35320098201043 L 979.6513671874998 447.42922717354156 L 980.6015624999999 447.5052533650727 L 981.5517578124999 447.5812795566039 L 982.5019531249999 447.657305748135 L 983.4521484374999 447.7333319396662 L 984.40234375 447.8093581311973 L 985.3525390625 447.8853843227284 L 986.302734375 447.96141051425957 L 987.2529296874999 448.0374367057907 L 988.2031249999999 448.1134628973218 L 989.1533203125 448.189489088853 L 990.1035156249999 448.2655152803841 L 991.0537109374999 448.3415414719152 L 992.0039062499999 448.4175676634464 L 992.9541015624999 448.4935938549775 L 993.904296875 448.56962004650865 L 994.8544921875 448.64564623803983 L 995.8046875 448.72167242957096 L 996.7548828125 448.79769862110203 L 997.7050781250001 448.8737248126332 L 998.6552734375 448.94975100416434 L 999.60546875 449.02577719569547 L 1000.5556640625 449.10180338722665 L 1001.5058593749999 449.1778295787577 L 1002.4560546874999 449.25385577028885 L 1003.40625 449.32988196182004 L 1004.3564453125 449.40590815335116 L 1005.306640625 449.4819343448823 L 1006.2568359374999 449.5579605364135 L 1007.2070312499999 449.6339867279446 L 1008.1572265625 449.7100129194757 L 1009.1074218749999 449.78603911100686 L 1010.0576171874999 449.862065302538 L 1011.0078124999999 449.9380914940691 L 1011.9580078124999 450.0141176856003 L 1012.908203125 450.09014387713137 L 1013.8583984374999 450.1661700686625 L 1014.8085937499999 450.2421962601937 L 1015.7587890624999 450.3182224517248 L 1016.7089843749998 450.39424864325593 L 1017.6591796874998 450.4702748347871 L 1018.6093749999999 450.5463010263182 L 1019.5595703124999 450.6223272178493 L 1020.5097656249999 450.6983534093805 L 1021.4599609374998 450.77437960091163 L 1022.4101562499998 450.85040579244276 L 1023.3603515624999 450.9264319839738 L 1024.3105468749998 451.002458175505 L 1025.2607421874998 451.07848436703614 L 1026.2109374999998 451.1545105585673 L 1027.1611328124998 451.23053675009845 L 1028.111328125 451.3065629416296 L 1029.0615234375 451.38258913316076 L 1030.01171875 451.45861532469183 L 1030.9619140625 451.53464151622296 L 1031.912109375 451.61066770775415 L 1032.8623046875 451.6866938992853 L 1033.8125 451.7627200908164 L 1034.7626953125 451.83874628234753 L 1035.7128906249998 451.91477247387866 L 1036.6630859374998 451.9907986654098 L 1037.61328125 452.06682485694097 L 1038.5634765625 452.1428510484721 L 1039.513671875 452.2188772400033 L 1040.4638671875 452.2949034315344 L 1041.4140625 452.3709296230655 L 1042.3642578125 452.4469558145966 L 1043.314453125 452.5229820061278 L 1044.2646484375 452.5990081976589 L 1045.21484375 452.6750343891901 L 1046.1650390625 452.7510605807212 L 1047.115234375 452.8270867722523 L 1048.0654296875 452.9031129637834 L 1049.015625 452.9791391553146 L 1049.9658203125 453.05516534684574 L 1050.916015625 453.1311915383769 L 1051.8662109375 453.20721772990805 L 1052.81640625 453.2832439214391 L 1053.7666015625 453.35927011297025 L 1054.7167968749998 453.43529630450143 L 1055.6669921874998 453.51132249603256 L 1056.6171875 453.58734868756375 L 1057.5673828125 453.6633748790948 L 1058.517578125 453.73940107062595 L 1059.4677734374998 453.8154272621571 L 1060.4179687499998 453.89145345368826 L 1061.3681640625 453.9674796452194 L 1062.3183593749998 454.04350583675057 L 1063.2685546874998 454.11953202828164 L 1064.2187499999998 454.19555821981277 L 1065.1689453124998 454.2715844113439 L 1066.119140625 454.3476106028751 L 1067.0693359374998 454.4236367944062 L 1068.0195312499998 454.4996629859373 L 1068.9697265624998 454.57568917746846 L 1069.9199218749995 454.6517153689996 L 1070.8701171874995 454.7277415605307 L 1071.8203124999998 454.8037677520619 L 1072.7705078124998 454.87979394359303 L 1073.7207031249998 454.9558201351242 L 1074.6708984374998 455.0318463266553 L 1075.62109375 455.1078725181864 L 1076.5712890625 455.18389870971754 L 1077.521484375 455.2599249012487 L 1078.4716796874998 455.33595109277985 L 1079.4218749999998 455.4119772843109 L 1080.3720703125 455.4880034758421 L 1081.3222656249998 455.56402966737323 L 1082.2724609374998 455.64005585890436 L 1083.2226562499998 455.71608205043555 L 1084.1728515624998 455.7921082419667 L 1085.123046875 455.86813443349786 L 1086.0732421875 455.9441606250289 L 1087.0234375 456.02018681656006 L 1087.9736328125 456.09621300809124 L 1088.923828125 456.17223919962237 L 1089.8740234375 456.2482653911535 L 1090.82421875 456.32429158268457 L 1091.7744140625 456.40031777421575 L 1092.7246093749998 456.4763439657469 L 1093.6748046874998 456.55237015727806 L 1094.625 456.6283963488092 L 1095.5751953125 456.7044225403403 L 1096.525390625 456.7804487318715 L 1097.4755859374998 456.8564749234026 L 1098.4257812499998 456.9325011149337 L 1099.3759765625 457.0085273064649 L 1100.3261718749998 457.084553497996 L 1101.2763671874998 457.16057968952714 L 1102.2265624999998 457.2366058810582 L 1103.1767578124998 457.3126320725894 L 1104.126953125 457.3886582641205 L 1105.0771484375 457.4646844556517 L 1106.02734375 457.54071064718283 L 1106.9775390625 457.61673683871396 L 1107.927734375 457.69276303024515 L 1108.8779296875 457.7687892217762 L 1109.828125 457.84481541330734 L 1110.7783203125 457.92084160483853 L 1111.7285156249998 457.99686779636966 L 1112.6787109374998 458.0728939879008 L 1113.62890625 458.14892017943185 L 1114.5791015625 458.22494637096304 L 1115.529296875 458.30097256249417 L 1116.4794921875 458.37699875402535 L 1117.4296875 458.4530249455565 L 1118.3798828125 458.5290511370876 L 1119.330078125 458.6050773286188 L 1120.2802734375 458.68110352014986 L 1121.23046875 458.757129711681 L 1122.1806640625 458.8331559032122 L 1123.130859375 458.9091820947433 L 1124.0810546875 458.9852082862744 L 1125.03125 459.0612344778055 L 1125.9814453125 459.1372606693367 L 1126.931640625 459.2132868608678 L 1127.8818359375 459.289313052399 L 1128.83203125 459.3653392439301 L 1129.7822265625 459.44136543546125 L 1130.7324218749998 459.5173916269923 L 1131.6826171874998 459.5934178185235 L 1132.6328124999998 459.66944401005463 L 1133.5830078125 459.7454702015858 L 1134.533203125 459.82149639311695 L 1135.4833984375 459.8975225846481 L 1136.43359375 459.9735487761792 L 1137.3837890625 460.0495749677103 L 1138.333984375 460.12560115924146 L 1139.2841796875 460.20162735077264 L 1140.234375 460.27765354230377 L 1141.1845703125 460.35367973383495 L 1142.1347656249998 460.429705925366 L 1143.0849609375 460.50573211689715 L 1144.03515625 460.5817583084283 L 1144.9853515625 460.65778449995946 L 1145.935546875 460.7338106914906 L 1146.8857421875 460.8098368830218 L 1147.8359375 460.8858630745529 L 1148.7861328125 460.961889266084 L 1149.736328125 461.0379154576151 L 1150.6865234375 461.1139416491463 L 1151.63671875 461.1899678406774 L 1152.5869140625 461.2659940322086 L 1153.537109375 461.3420202237397 L 1154.4873046875 461.4180464152708 L 1155.4375 461.4940726068019 L 1156.3876953125 461.5700987983331 L 1157.337890625 461.64612498986423 L 1158.2880859375 461.7221511813954 L 1159.23828125 461.7981773729265 L 1160.1884765625 461.8742035644576 L 1161.138671875 461.95022975598874 L 1162.0888671875 462.0262559475199 L 1163.0390625 462.10228213905106 L 1163.9892578125 462.17830833058224 L 1164.939453125 462.25433452211337 L 1165.8896484375 462.33036071364444 L 1166.83984375 462.40638690517557 L 1167.7900390625 462.48241309670675 L 1168.740234375 462.5584392882379 L 1169.6904296875 462.63446547976906 L 1170.640625 462.71049167130013 L 1171.5908203125 462.78651786283126 L 1172.541015625 462.8625440543624 L 1173.4912109375 462.9385702458936 L 1174.44140625 463.0145964374247 L 1175.3916015625 463.0906226289559 L 1176.341796875 463.166648820487 L 1177.2919921875 463.2426750120181 L 1178.2421875 463.3187012035492 L 1179.1923828125 463.3947273950804 L 1180.142578125 463.4707535866115 L 1181.0927734375 463.5467797781427 L 1182.04296875 463.6228059696738 L 1182.9931640625 463.6988321612049 L 1183.943359375 463.77485835273603 L 1184.8935546875 463.8508845442672 L 1185.84375 463.92691073579834 L 1186.7939453125 464.00293692732953 L 1187.744140625 464.07896311886066 L 1188.6943359375 464.1549893103917 L 1189.64453125 464.2310155019229 L 1190.5947265625 464.30704169345404 L 1191.544921875 464.38306788498517 L 1192.4951171875 464.45909407651635 L 1193.4453125 464.5351202680474 L 1194.3955078125 464.61114645957855 L 1195.345703125 464.68717265110973 L 1196.2958984375 464.76319884264086 L 1197.24609375 464.839225034172 L 1198.1962890625 464.9152512257032 L 1199.146484375 464.99127741723424 L 1200.0966796875 465.06730360876537 L 1201.046875 465.14332980029656 L 1201.9970703125 465.2193559918277 L 1202.947265625 465.2953821833588 L 1203.8974609375 465.3714083748899 L 1204.84765625 465.44743456642107 L 1205.7978515625 465.5234607579522 L 1206.7480468749995 465.5994869494834 L 1207.6982421875 465.6755131410145 L 1208.6484375 465.75153933254563 L 1209.5986328125 465.8275655240768 L 1210.548828125 465.9035917156079 L 1211.4990234375 465.979617907139 L 1212.44921875 466.0556440986702 L 1213.3994140625 466.1316702902013 L 1214.349609375 466.20769648173246 L 1215.2998046875 466.2837226732635 L 1216.25 466.3597488647947 L 1217.2001953125 466.43577505632584 L 1218.150390625 466.511801247857 L 1219.1005859375 466.58782743938815 L 1220.05078125 466.6638536309193 L 1221.0009765625 466.73987982245046 L 1221.951171875 466.81590601398153 L 1222.9013671875 466.89193220551266 L 1223.8515625 466.96795839704384 L 1224.8017578125 467.043984588575 L 1225.751953125 467.1200107801061 L 1226.7021484375 467.19603697163717 L 1227.65234375 467.27206316316835 L 1228.6025390625 467.3480893546995 L 1229.552734375 467.42411554623067 L 1230.5029296875 467.5001417377618 L 1231.453125 467.5761679292929 L 1232.4033203125 467.6521941208241 L 1233.353515625 467.72822031235523 L 1234.3037109375 467.8042465038863 L 1235.25390625 467.8802726954175 L 1236.2041015625 467.9562988869486 L 1237.154296875 468.0323250784797 L 1238.1044921875 468.10835127001087 L 1239.0546875 468.184377461542 L 1240.0048828125 468.2604036530731 L 1240.955078125 468.3364298446043 L 1241.9052734375 468.41245603613544 L 1242.85546875 468.4884822276666 L 1243.8056640625 468.56450841919775 L 1244.7558593749995 468.6405346107288 L 1245.7060546875 468.71656080225995 L 1246.65625 468.79258699379113 L 1247.6064453125 468.86861318532226 L 1248.556640625 468.94463937685333 L 1249.5068359374995 469.0206655683845 L 1250.45703125 469.09669175991564 L 1251.4072265625 469.17271795144677 L 1252.3574218749995 469.24874414297796 L 1253.3076171874995 469.3247703345091 L 1254.2578124999995 469.40079652604027 L 1255.2080078125 469.47682271757134 L 1256.158203125 469.55284890910247 L 1257.1083984375 469.6288751006336 L 1258.05859375 469.7049012921648 L 1259.0087890625 469.7809274836959 L 1259.958984375 469.8569536752271 L 1260.9091796875 469.93297986675816 L 1261.859375 470.0090060582893 L 1262.8095703125 470.0850322498204 L 1263.7597656249995 470.1610584413516 L 1264.7099609375 470.2370846328827 L 1265.66015625 470.3131108244139 L 1266.6103515625 470.38913701594504 L 1267.560546875 470.4651632074761 L 1268.5107421875 470.54118939900724 L 1269.4609375 470.6172155905384 L 1270.4111328125 470.69324178206955 L 1271.361328125 470.76926797360073 L 1272.3115234375 470.8452941651318 L 1273.26171875 470.92132035666293 L 1274.2119140625 470.99734654819406 L 1275.162109375 471.07337273972524 L 1276.1123046875 471.14939893125637 L 1277.0625 471.22542512278756 L 1278.0126953125 471.3014513143187 L 1278.962890625 471.37747750584975 L 1279.9130859375 471.4535036973809 L 1280.86328125 471.52952988891207 L 1281.8134765625 471.6055560804432 L 1282.7636718749995 471.68158227197426 L 1283.7138671875 471.75760846350545 L 1284.6640625 471.8336346550366 L 1285.6142578125 471.9096608465677 L 1286.564453125 471.9856870380989 L 1287.5146484375 472.06171322963 L 1288.46484375 472.1377394211612 L 1289.4150390625 472.2137656126923 L 1290.365234375 472.2897918042234 L 1291.3154296875 472.3658179957546 L 1292.265625 472.4418441872857 L 1293.2158203125 472.51787037881684 L 1294.166015625 472.5938965703479 L 1295.1162109375 472.6699227618791 L 1296.06640625 472.7459489534102 L 1297.0166015625 472.8219751449414 L 1297.966796875 472.89800133647253 L 1298.9169921875 472.97402752800366 L 1299.8671875 473.05005371953484 L 1300.8173828125 473.126079911066 L 1301.767578125 473.20210610259704 L 1302.7177734375 473.2781322941282 L 1303.66796875 473.35415848565935 L 1304.6181640625 473.4301846771905 L 1305.568359375 473.50621086872155 L 1306.5185546875 473.58223706025274 L 1307.46875 473.65826325178386 L 1308.4189453125 473.73428944331505 L 1309.369140625 473.8103156348462 L 1310.3193359375 473.8863418263773 L 1311.26953125 473.9623680179085 L 1312.2197265625 474.03839420943956 L 1313.169921875 474.1144204009707 L 1314.1201171875 474.19044659250187 L 1315.0703125 474.266472784033 L 1316.0205078125 474.3424989755641 L 1316.970703125 474.4185251670952 L 1317.9208984375 474.4945513586264 L 1318.87109375 474.5705775501575 L 1319.8212890625 474.6466037416887 L 1320.771484375 474.7226299332198 L 1321.7216796875 474.79865612475095 L 1322.671875 474.87468231628213 L 1323.6220703125 474.95070850781326 L 1324.572265625 475.02673469934433 L 1325.5224609375 475.1027608908755 L 1326.47265625 475.17878708240664 L 1327.4228515625 475.25481327393777 L 1328.373046875 475.33083946546884 L 1329.3232421875 475.406865657 L 1330.2734375 475.48289184853115 L 1331.2236328125 475.55891804006234 L 1332.173828125 475.63494423159347 L 1333.1240234375 475.7109704231246 L 1334.07421875 475.7869966146558 L 1335.0244140625 475.8630228061869 L 1335.974609375 475.939048997718 L 1336.9248046875 476.01507518924916 L 1337.875 476.0911013807803 L 1338.8251953125 476.1671275723114 L 1339.775390625 476.24315376384254 L 1340.7255859375 476.31917995537367 L 1341.67578125 476.3952061469048 L 1342.6259765625 476.471232338436 L 1343.576171875 476.5472585299671 L 1344.5263671875 476.6232847214983 L 1345.4765625 476.6993109130294 L 1346.4267578125 476.7753371045605 L 1347.376953125 476.8513632960916 L 1348.3271484375 476.9273894876228 L 1349.27734375 477.00341567915393 L 1350.2275390625 477.0794418706851 L 1351.177734375 477.15546806221624 L 1352.1279296875 477.2314942537473 L 1353.078125 477.30752044527844 L 1354.0283203125 477.3835466368096 L 1354.978515625 477.45957282834075 L 1355.9287109375 477.53559901987194 L 1356.87890625 477.61162521140307 L 1357.8291015625 477.68765140293414 L 1358.779296875 477.76367759446526 L 1359.7294921875 477.83970378599645 L 1360.6796875 477.9157299775276 L 1361.6298828125 477.99175616905876 L 1362.580078125 478.0677823605899 L 1363.5302734375005 478.143808552121 L 1364.48046875 478.2198347436521 L 1365.4306640625 478.29586093518327 L 1366.380859375 478.3718871267144 L 1367.3310546875 478.4479133182456 L 1368.28125 478.5239395097767 L 1369.2314453125 478.59996570130784 L 1370.181640625 478.6759918928389 L 1371.1318359375 478.7520180843701 L 1372.08203125 478.8280442759012 L 1373.0322265624995 478.9040704674323 L 1373.982421875 478.9800966589635 L 1374.9326171875 479.0561228504946 L 1375.8828125 479.13214904202573 L 1376.8330078125 479.2081752335569 L 1377.783203125 479.28420142508804 L 1378.7333984375 479.3602276166192 L 1379.68359375 479.43625380815035 L 1380.6337890625 479.5122799996814 L 1381.583984375 479.58830619121255 L 1382.5341796875005 479.66433238274374 L 1383.484375 479.74035857427486 L 1384.4345703125 479.81638476580605 L 1385.3847656250005 479.8924109573372 L 1386.3349609375005 479.9684371488683 L 1387.2851562500005 480.0444633403994 L 1388.2353515625 480.12048953193056 L 1389.185546875 480.1965157234617 L 1390.1357421875 480.27254191499287 L 1391.0859375 480.348568106524 L 1392.0361328125005 480.4245942980551 L 1392.986328125 480.50062048958625 L 1393.9365234375 480.5766466811174 L 1394.88671875 480.6526728726485 L 1395.8369140625 480.7286990641796 L 1396.787109375 480.80472525571076 L 1397.7373046875 480.8807514472419 L 1398.6875 480.9567776387731 L 1399.6376953125 481.0328038303042 L 1400.587890625 481.10883002183533 L 1401.5380859375005 481.1848562133665 L 1402.48828125 481.26088240489764 L 1403.4384765625 481.3369085964287 L 1404.388671875 481.4129347879599 L 1405.3388671875 481.488960979491 L 1406.2890625 481.56498717102215 L 1407.2392578125 481.64101336255334 L 1408.189453125 481.7170395540844 L 1409.1396484375 481.79306574561554 L 1410.08984375 481.8690919371467 L 1411.0400390624995 481.94511812867785 L 1411.990234375 482.021144320209 L 1412.9404296875 482.09717051174016 L 1413.890625 482.1731967032713 L 1414.8408203125 482.24922289480236 L 1415.791015625 482.32524908633354 L 1416.7412109375 482.40127527786467 L 1417.69140625 482.4773014693958 L 1418.6416015625 482.55332766092687 L 1419.591796875 482.62935385245805 L 1420.5419921874995 482.7053800439892 L 1421.4921875 482.78140623552036 L 1422.4423828125 482.8574324270515 L 1423.392578125 482.9334586185826 L 1424.3427734375 483.0094848101138 L 1425.2929687499995 483.0855110016449 L 1426.2431640624995 483.161537193176 L 1427.193359375 483.2375633847072 L 1428.1435546875 483.3135895762383 L 1429.09375 483.3896157677694 L 1430.0439453124995 483.4656419593005 L 1430.994140625 483.5416681508317 L 1431.9443359375 483.6176943423628 L 1432.89453125 483.693720533894 L 1433.8447265625 483.76974672542514 L 1434.7949218749995 483.84577291695626 L 1435.7451171874995 483.92179910848733 L 1436.6953125 483.9978253000185 L 1437.6455078125 484.07385149154965 L 1438.595703125 484.14987768308083 L 1439.5458984374995 484.2259038746119 L 1440.4960937499995 484.30193006614303 L 1441.4462890624995 484.3779562576742 L 1442.3964843749995 484.45398244920534 L 1443.3466796875 484.53000864073647 L 1444.2968749999995 484.60603483226765 L 1445.2470703124995 484.6820610237988 L 1446.197265625 484.75808721532997 L 1447.1474609375 484.8341134068611 L 1448.09765625 484.91013959839216 L 1449.0478515624995 484.9861657899233 L 1449.998046875 485.0621919814545 L 1450.9482421875 485.1382181729856 L 1451.8984375 485.2142443645168 L 1452.8486328125 485.29027055604786 L 1453.798828125 485.366296747579 L 1454.7490234375 485.4423229391101 L 1455.69921875 485.5183491306413 L 1456.6494140625 485.5943753221724 L 1457.599609375 485.6704015137036 L 1458.5498046874995 485.7464277052347 L 1459.5 485.8224538967658 L 1460.4501953125 485.89848008829694 L 1461.400390625 485.9745062798281 L 1462.3505859375 486.05053247135925 L 1463.3007812499995 486.1265586628903 L 1464.2509765624995 486.2025848544215 L 1465.201171875 486.27861104595263 L 1466.1513671875 486.35463723748376 L 1467.1015625 486.43066342901494 L 1468.0517578124995 486.50668962054607 L 1469.001953125 486.58271581207725 L 1469.9521484375 486.6587420036084 L 1470.90234375 486.73476819513945 L 1471.8525390625 486.8107943866706 L 1472.802734375 486.88682057820176 L 1473.7529296875 486.9628467697329 L 1474.703125 487.0388729612641 L 1475.6533203125 487.11489915279515 L 1476.603515625 487.1909253443263 L 1477.5537109375005 487.2669515358574 L 1478.50390625 487.3429777273886 L 1479.4541015625 487.4190039189197 L 1480.404296875 487.4950301104509 L 1481.3544921875 487.57105630198197 L 1482.3046875 487.6470824935131 L 1483.2548828125 487.7231086850442 L 1484.205078125 487.7991348765754 L 1485.1552734375 487.87516106810654 L 1486.10546875 487.9511872596376 L 1487.0556640624995 488.0272134511688 L 1488.005859375 488.1032396426999 L 1488.9560546875 488.17926583423105 L 1489.90625 488.25529202576223 L 1490.8564453125 488.33131821729336 L 1491.806640625 488.40734440882454 L 1492.7568359375 488.48337060035567 L 1493.70703125 488.55939679188674 L 1494.6572265625 488.6354229834179 L 1495.607421875 488.71144917494905 L 1496.5576171874995 488.7874753664801 L 1497.5078125 488.86350155801125 L 1498.4580078125 488.93952774954244 L 1499.408203125 489.01555394107356 L 1500.3583984375 489.09158013260475 L 1501.3085937499995 489.1676063241359 L 1502.2587890624995 489.243632515667 L 1503.208984375 489.3196587071982 L 1504.1591796875 489.3956848987293 L 1505.109375 489.4717110902604 L 1506.0595703124995 489.54773728179157 L 1507.009765625 489.6237634733227 L 1507.9599609375 489.6997896648538 L 1508.91015625 489.7758158563849 L 1509.8603515625 489.8518420479161 L 1510.8105468749995 489.9278682394472 L 1511.7607421874995 490.0038944309784 L 1512.7109375 490.0799206225095 L 1513.6611328125 490.15594681404065 L 1514.611328125 490.23197300557183 L 1515.5615234374995 490.3079991971029 L 1516.5117187499995 490.38402538863403 L 1517.4619140624995 490.4600515801651 L 1518.4121093749995 490.5360777716963 L 1519.3623046875 490.6121039632274 L 1520.3124999999995 490.68813015475854 L 1521.2626953124995 490.7641563462897 L 1522.212890625 490.84018253782085 L 1523.1630859375 490.91620872935204 L 1524.11328125 490.99223492088316 L 1525.0634765624995 491.0682611124143 L 1526.0136718749995 491.14428730394536 L 1526.9638671874995 491.22031349547655 L 1527.9140624999995 491.2963396870077 L 1528.8642578125 491.37236587853886 L 1529.8144531249995 491.44839207006993 L 1530.7646484374995 491.52441826160106 L 1531.7148437499995 491.6004444531322 L 1532.6650390624995 491.67647064466337 L 1533.6152343749995 491.7524968361945 L 1534.5654296874995 491.8285230277257 L 1535.5156249999995 491.9045492192568 L 1536.4658203124995 491.9805754107879 L 1537.4160156249995 492.056601602319 L 1538.3662109375 492.1326277938502 L 1539.3164062499995 492.2086539853813 L 1540.2666015624995 492.2846801769125 L 1541.216796875 492.36070636844363 L 1542.1669921875 492.43673255997476 L 1543.1171875 492.5127587515058 L 1544.0673828124995 492.588784943037 L 1545.017578125 492.66481113456814 L 1545.9677734375 492.7408373260993 L 1546.91796875 492.81686351763045 L 1547.8681640625 492.89288970916164 L 1548.8183593749995 492.9689159006927 L 1549.7685546874995 493.04494209222383 L 1550.71875 493.12096828375496 L 1551.6689453125 493.19699447528615 L 1552.619140625 493.2730206668173 L 1553.5693359374995 493.34904685834834 L 1554.5195312499995 493.42507304987953 L 1555.4697265624995 493.50109924141066 L 1556.4199218749995 493.5771254329418 L 1557.3701171875 493.65315162447297 L 1558.3203124999995 493.7291778160041 L 1559.2705078124995 493.80520400753517 L 1560.220703125 493.88123019906635 L 1561.1708984375 493.9572563905975 L 1562.12109375 494.0332825821286 L 1563.0712890624995 494.1093087736598 L 1564.021484375 494.1853349651909 L 1564.9716796875 494.2613611567221 L 1565.921875 494.3373873482532 L 1566.8720703125 494.4134135397843 L 1567.822265625 494.48943973131543 L 1568.7724609375 494.5654659228466 L 1569.72265625 494.64149211437774 L 1570.6728515625 494.7175183059089 L 1571.623046875 494.79354449744 L 1572.5732421874995 494.8695706889711 L 1573.5234375 494.94559688050225 L 1574.4736328125 495.02162307203344 L 1575.423828125 495.09764926356456 L 1576.3740234375 495.17367545509563 L 1577.3242187499995 495.2497016466268 L 1578.2744140624995 495.32572783815795 L 1579.224609375 495.4017540296891 L 1580.1748046875 495.47778022122026 L 1581.125 495.5538064127514 L 1582.0751953124995 495.62983260428246 L 1583.025390625 495.70585879581364 L 1583.9755859375 495.78188498734477 L 1584.92578125 495.8579111788759 L 1585.8759765625 495.9339373704071 L 1586.8261718749995 496.00996356193815 L 1587.7763671874995 496.0859897534693 L 1588.7265625 496.16201594500046 L 1589.6767578125 496.2380421365316 L 1590.626953125 496.3140683280627 L 1591.5771484374995 496.3900945195939 L 1592.5273437499995 496.466120711125 L 1593.4775390624995 496.5421469026561 L 1594.4277343749995 496.6181730941873 L 1595.3779296875 496.6941992857184 L 1596.3281249999995 496.77022547724954 L 1597.2783203124995 496.84625166878067 L 1598.228515625 496.9222778603118 L 1599.1787109375 496.9983040518429 L 1600.12890625 497.0743302433741 L 1601.0791015624995 497.15035643490523 L 1602.029296875 497.2263826264364 L 1602.9794921875 497.30240881796755 L 1603.9296875 497.3784350094987 L 1604.8798828125 497.45446120102986 L 1605.830078125 497.530487392561 L 1606.7802734375 497.60651358409217 L 1607.73046875 497.68253977562324 L 1608.6806640625 497.75856596715437 L 1609.630859375 497.83459215868544 L 1610.5810546874995 497.91061835021657 L 1611.53125 497.98664454174775 L 1612.4814453125 498.0626707332789 L 1613.431640625 498.13869692481006 L 1614.3818359375 498.2147231163412 L 1615.3320312499995 498.2907493078723 L 1616.2822265624995 498.3667754994034 L 1617.232421875 498.4428016909346 L 1618.1826171875 498.5188278824657 L 1619.1328125 498.5948540739969 L 1620.0830078124995 498.67088026552796 L 1621.033203125 498.7469064570591 L 1621.9833984375 498.8229326485902 L 1622.93359375 498.8989588401214 L 1623.8837890625 498.9749850316525 L 1624.833984375 499.0510112231837 L 1625.7841796875 499.12703741471483 L 1626.734375 499.20306360624596 L 1627.6845703125 499.27908979777715 L 1628.634765625 499.3551159893083 L 1629.5849609375005 499.43114218083946 L 1630.53515625 499.50716837237053 L 1631.4853515625 499.58319456390166 L 1632.435546875 499.6592207554328 L 1633.3857421875 499.73524694696385 L 1634.3359375 499.81127313849504 L 1635.2861328125 499.88729933002617 L 1636.236328125 499.96332552155735 L 1637.1865234375 500.0393517130885 L 1638.13671875 500.1153779046196 L 1639.0869140624995 500.1914040961507 L 1640.037109375 500.26743028768186 L 1640.9873046875 500.343456479213 L 1641.9375 500.4194826707442 L 1642.8876953125 500.4955088622753 L 1643.837890625 500.57153505380643 L 1644.7880859375 500.6475612453376 L 1645.73828125 500.7235874368687 L 1646.6884765625 500.7996136283998 L 1647.638671875 500.875639819931 L 1648.5888671874995 500.9516660114621 L 1649.5390625 501.02769220299325 L 1650.4892578125 501.10371839452444 L 1651.439453125 501.1797445860555 L 1652.3896484375 501.25577077758663 L 1653.3398437499995 501.3317969691178 L 1654.2900390624995 501.4078231606489 L 1655.240234375 501.48384935218 L 1656.1904296875 501.5598755437112 L 1657.140625 501.6359017352423 L 1658.0908203124995 501.71192792677346 L 1659.041015625 501.78795411830464 L 1659.9912109375 501.86398030983577 L 1660.94140625 501.94000650136695 L 1661.8916015625 502.016032692898 L 1662.841796875 502.09205888442915 L 1663.7919921875 502.1680850759603 L 1664.7421875 502.24411126749146 L 1665.6923828125 502.3201374590226 L 1666.642578125 502.3961636505538 L 1667.5927734375005 502.4721898420849 L 1668.54296875 502.548216033616 L 1669.4931640625 502.6242422251471 L 1670.443359375 502.7002684166783 L 1671.3935546875 502.7762946082094 L 1672.34375 502.8523207997406 L 1673.2939453125 502.9283469912717 L 1674.244140625 503.0043731828028 L 1675.1943359375 503.0803993743339 L 1676.14453125 503.1564255658651 L 1677.0947265624995 503.2324517573962 L 1678.044921875 503.3084779489273 L 1678.9951171875 503.3845041404585 L 1679.9453125 503.4605303319896 L 1680.8955078125 503.53655652352074 L 1681.845703125 503.61258271505193 L 1682.7958984375 503.68860890658306 L 1683.74609375 503.76463509811424 L 1684.6962890625 503.8406612896453 L 1685.646484375 503.91668748117644 L 1686.5966796875005 503.99271367270757 L 1687.546875 504.06873986423875 L 1688.4970703125 504.1447660557699 L 1689.447265625 504.22079224730106 L 1690.3974609375005 504.2968184388322 L 1691.3476562500005 504.37284463036326 L 1692.2978515625 504.4488708218944 L 1693.248046875 504.5248970134256 L 1694.1982421875 504.6009232049567 L 1695.1484375 504.6769493964879 L 1696.0986328125005 504.752975588019 L 1697.048828125 504.82900177955014 L 1697.9990234375 504.9050279710812 L 1698.94921875 504.9810541626124 L 1699.8994140625 505.05708035414347 L 1700.849609375 505.1331065456746 L 1701.7998046875 505.2091327372058 L 1702.75 505.2851589287369 L 1703.7001953125 505.3611851202681 L 1704.650390625 505.4372113117992 L 1705.6005859375005 505.51323750333034 L 1706.55078125 505.58926369486153 L 1707.5009765625 505.66528988639266 L 1708.451171875 505.7413160779237 L 1709.4013671875 505.8173422694549 L 1710.3515625 505.89336846098604 L 1711.3017578125 505.96939465251717 L 1712.251953125 506.04542084404824 L 1713.2021484375 506.1214470355794 L 1714.15234375 506.19747322711055 L 1715.1025390624995 506.27349941864173 L 1716.052734375 506.34952561017286 L 1717.0029296875 506.425551801704 L 1717.953125 506.5015779932352 L 1718.9033203125 506.57760418476624 L 1719.853515625 506.6536303762974 L 1720.8037109375 506.72965656782856 L 1721.75390625 506.8056827593597 L 1722.7041015625 506.88170895089075 L 1723.654296875 506.9577351424219 L 1724.6044921875005 507.03376133395307 L 1725.5546875 507.1097875254842 L 1726.5048828125 507.1858137170154 L 1727.455078125 507.2618399085465 L 1728.4052734375005 507.33786610007763 L 1729.3554687500005 507.4138922916088 L 1730.3056640625 507.48991848313995 L 1731.255859375 507.565944674671 L 1732.2060546875 507.6419708662022 L 1733.15625 507.7179970577333 L 1734.1064453125005 507.79402324926446 L 1735.056640625 507.87004944079564 L 1736.0068359375 507.9460756323267 L 1736.95703125 508.02210182385784 L 1737.9072265625 508.098128015389 L 1738.857421875 508.17415420692015 L 1739.8076171875 508.2501803984513 L 1740.7578125 508.32620658998246 L 1741.7080078125 508.40223278151353 L 1742.658203125 508.47825897304466 L 1743.6083984375005 508.55428516457584 L 1744.55859375 508.630311356107 L 1745.5087890625 508.7063375476381 L 1746.458984375 508.7823637391693 L 1747.4091796875005 508.8583899307004 L 1748.3593750000005 508.9344161222315 L 1749.3095703125 509.01044231376267 L 1750.2597656250005 509.0864685052938 L 1751.2099609375005 509.1624946968249 L 1752.1601562500005 509.2385208883561 L 1753.1103515625005 509.31454707988723 L 1754.060546875 509.3905732714183 L 1755.0107421875 509.4665994629495 L 1755.9609375 509.5426256544806 L 1756.9111328125005 509.6186518460118 L 1757.8613281250005 509.69467803754293 L 1758.8115234375 509.770704229074 L 1759.76171875 509.8467304206051 L 1760.7119140625 509.9227566121363 L 1761.662109375 509.99878280366744 L 1762.6123046875005 510.0748089951986 L 1763.5625 510.15083518672975 L 1764.5126953125 510.2268613782608 L 1765.462890625 510.30288756979195 L 1766.4130859375005 510.37891376132313 L 1767.3632812500005 510.45493995285426 L 1768.3134765625 510.53096614438545 L 1769.263671875 510.6069923359165 L 1770.2138671875 510.68301852744764 L 1771.1640625 510.75904471897877 L 1772.1142578125005 510.83507091050996 L 1773.064453125 510.9110971020411 L 1774.0146484375 510.98712329357227 L 1774.96484375 511.06314948510334 L 1775.9150390625 511.13917567663447 L 1776.865234375 511.2152018681656 L 1777.8154296875 511.2912280596968 L 1778.765625 511.3672542512279 L 1779.7158203125 511.443280442759 L 1780.666015625 511.51930663429016 L 1781.6162109375005 511.5953328258213 L 1782.56640625 511.6713590173524 L 1783.5166015625 511.7473852088836 L 1784.466796875 511.8234114004147 L 1785.4169921875 511.8994375919459 L 1786.3671875 511.97546378347704 L 1787.3173828125 512.0514899750082 L 1788.267578125 512.1275161665392 L 1789.2177734375 512.2035423580704 L 1790.16796875 512.2795685496014 L 1791.1181640624995 512.3555947411326 L 1792.068359375 512.4316209326638 L 1793.0185546875 512.5076471241949 L 1793.96875 512.5836733157261 L 1794.9189453125 512.6596995072573 L 1795.869140625 512.7357256987884 L 1796.8193359375 512.8117518903196 L 1797.76953125 512.8877780818507 L 1798.7197265625 512.9638042733818 L 1799.669921875 513.0398304649129 L 1800.6201171874995 513.1158566564441 L 1801.5703125 513.1918828479752 L 1802.5205078125 513.2679090395063 L 1803.470703125 513.3439352310374 L 1804.4208984375 513.4199614225686 L 1805.3710937499995 513.4959876140997 L 1806.3212890624995 513.5720138056308 L 1807.2714843749995 513.648039997162 L 1808.2216796875 513.7240661886932 L 1809.171875 513.8000923802242 L 1810.1220703124995 513.8761185717553 L 1811.072265625 513.9521447632866 L 1812.0224609375 514.0281709548177 L 1812.97265625 514.1041971463487 L 1813.9228515625 514.1802233378799 L 1814.873046875 514.2562495294111 L 1815.8232421875 514.3322757209422 L 1816.7734375 514.4083019124735 L 1817.7236328125 514.4843281040046 L 1818.673828125 514.5603542955357 L 1819.6240234375005 514.6363804870668 L 1820.57421875 514.712406678598 L 1821.5244140625 514.7884328701291 L 1822.474609375 514.8644590616602 L 1823.4248046875 514.9404852531914 L 1824.375 515.0165114447225 L 1825.3251953125 515.0925376362536 L 1826.275390625 515.1685638277847 L 1827.2255859375 515.2445900193159 L 1828.17578125 515.320616210847 L 1829.1259765624995 515.3966424023781 L 1830.076171875 515.4726685939092 L 1831.0263671875 515.5486947854405 L 1831.9765625 515.6247209769715 L 1832.9267578125 515.7007471685026 L 1833.876953125 515.7767733600339 L 1834.8271484375 515.852799551565 L 1835.77734375 515.9288257430961 L 1836.7275390625 516.0048519346271 L 1837.677734375 516.0808781261584 L 1838.6279296875005 516.1569043176895 L 1839.578125 516.2329305092208 L 1840.5283203125 516.3089567007519 L 1841.478515625 516.384982892283 L 1842.4287109375005 516.4610090838141 L 1843.3789062500005 516.5370352753453 L 1844.3291015625 516.6130614668764 L 1845.279296875 516.6890876584075 L 1846.2294921875 516.7651138499386 L 1847.1796875 516.8411400414698 L 1848.1298828125005 516.9171662330009 L 1849.080078125 516.993192424532 L 1850.0302734375 517.0692186160632 L 1850.98046875 517.1452448075943 L 1851.9306640625 517.2212709991254 L 1852.880859375 517.2972971906565 L 1853.8310546875 517.3733233821877 L 1854.78125 517.4493495737188 L 1855.7314453125 517.5253757652499 L 1856.681640625 517.6014019567812 L 1857.6318359375005 517.6774281483123 L 1858.58203125 517.7534543398435 L 1859.5322265625 517.8294805313745 L 1860.482421875 517.9055067229057 L 1861.4326171875 517.9815329144368 L 1862.3828125 518.057559105968 L 1863.3330078125 518.1335852974992 L 1864.283203125 518.2096114890303 L 1865.2333984375 518.2856376805614 L 1866.18359375 518.3616638720925 L 1867.1337890624995 518.4376900636237 L 1868.083984375 518.5137162551548 L 1869.0341796875 518.5897424466859 L 1869.984375 518.6657686382171 L 1870.9345703125 518.7417948297482 L 1871.884765625 518.8178210212793 L 1872.8349609375 518.8938472128104 L 1873.78515625 518.9698734043416 L 1874.7353515625 519.0458995958727 L 1875.685546875 519.1219257874038 L 1876.6357421874995 519.197951978935 L 1877.5859375 519.2739781704661 L 1878.5361328125 519.3500043619972 L 1879.486328125 519.4260305535284 L 1880.4365234375 519.5020567450596 L 1881.3867187499995 519.5780829365906 L 1882.3369140624995 519.6541091281218 L 1883.2871093749995 519.730135319653 L 1884.2373046875 519.8061615111841 L 1885.1875 519.8821877027153 L 1886.1376953124995 519.9582138942465 L 1887.087890625 520.0342400857776 L 1888.0380859375 520.1102662773087 L 1888.98828125 520.1862924688398 L 1889.9384765625 520.262318660371 L 1890.8886718749995 520.3383448519021 L 1891.8388671874995 520.4143710434332 L 1892.7890624999995 520.4903972349643 L 1893.7392578125 520.5664234264955 L 1894.689453125 520.6424496180266 L 1895.6396484374995 520.7184758095577 L 1896.5898437499995 520.7945020010889 L 1897.5400390624995 520.87052819262 L 1898.4902343749995 520.9465543841511 L 1899.4404296875 521.0225805756822 L 1900.3906249999995 521.0986067672134 L 1901.3408203124995 521.1746329587445 L 1902.2910156249995 521.2506591502756 L 1903.2412109375 521.3266853418069 L 1904.19140625 521.4027115333379 L 1905.1416015624995 521.4787377248691 L 1906.091796875 521.5547639164002 L 1907.0419921875 521.6307901079315 L 1907.9921875 521.7068162994626 L 1908.9423828125 521.7828424909937 L 1909.892578125 521.8588686825249 L 1910.8427734375 521.934894874056 L 1911.79296875 522.0109210655871 L 1912.7431640625 522.0869472571183 L 1913.693359375 522.1629734486494 L 1914.6435546874995 522.2389996401805 L 1915.59375 522.3150258317116 L 1916.5439453125 522.3910520232428 L 1917.494140625 522.4670782147739 L 1918.4443359375 522.543104406305 L 1919.3945312499995 522.6191305978361 L 1920.3447265624995 522.6951567893673 L 1921.2949218749995 522.7711829808984 L 1922.2451171875 522.8472091724295 L 1923.1953125 522.9232353639607 L 1924.1455078124995 522.9992615554919 L 1925.095703125 523.075287747023 L 1926.0458984375 523.1513139385542 L 1926.99609375 523.2273401300853 L 1927.9462890625 523.3033663216164 L 1928.896484375 523.3793925131475 L 1929.8466796875 523.4554187046788 L 1930.796875 523.5314448962099 L 1931.7470703125 523.607471087741 L 1932.697265625 523.6834972792722 L 1933.6474609375005 523.7595234708033 L 1934.59765625 523.8355496623344 L 1935.5478515625 523.9115758538655 L 1936.498046875 523.9876020453967 L 1937.4482421875 524.0636282369278 L 1938.3984375 524.1396544284589 L 1939.3486328125 524.21568061999 L 1940.298828125 524.2917068115212 L 1941.2490234375 524.3677330030523 L 1942.19921875 524.4437591945834 L 1943.1494140624995 524.5197853861146 L 1944.099609375 524.5958115776457 L 1945.0498046875 524.6718377691768 L 1946 524.747863960708" display="inline"></path><path id="jxgboxPoly_jxgBoard1G45" stroke-linecap="round" stroke-linejoin="round" style="position: absolute; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: inherit;" stroke="blue" stroke-opacity="1" stroke-width="1px" fill-opacity="0" d=" M 0 1339.2436649273038 L 0.9501953124999858 1330.4750574140332 L 1.900390625 1321.7488300613677 L 2.8505859375 1313.064875134667 L 3.80078125 1304.423085017228 L 4.750976562499986 1295.8233522102832 L 5.701171874999986 1287.2655693330034 L 6.651367187499986 1278.7496291224948 L 7.601562499999986 1270.2754244338005 L 8.5517578125 1261.842848239901 L 9.501953124999986 1253.4517936317134 L 10.452148437499986 1245.102153818091 L 11.402343749999972 1236.7938221258235 L 12.352539062499972 1228.5266919996384 L 13.302734374999986 1220.300657002199 L 14.252929687499986 1212.1156108141056 L 15.203124999999986 1203.9714472338958 L 16.15332031249997 1195.868060178043 L 17.103515624999986 1187.8053436809575 L 18.0537109375 1179.7831918949869 L 19.003906249999986 1171.801499090415 L 19.954101562499986 1163.8601596554624 L 20.904296875 1155.9590680962863 L 21.8544921875 1148.0981190369807 L 22.8046875 1140.277207219577 L 23.754882812499986 1132.4962275040418 L 24.705078125 1124.7550748682795 L 25.655273437500014 1117.0536444081313 L 26.60546875 1109.3918313373747 L 27.5556640625 1101.7695309877238 L 28.505859374999986 1094.1866388088297 L 29.456054687499986 1086.6430503682805 L 30.40625 1079.1386613515997 L 31.3564453125 1071.6733675622493 L 32.306640625 1064.247064921627 L 33.256835937499986 1056.8596494690673 L 34.207031249999986 1049.5110173618414 L 35.15722656249997 1042.2010648751575 L 36.107421874999986 1034.9296884021599 L 37.0576171875 1027.6967844539301 L 38.007812499999986 1020.5022496594868 L 38.958007812499986 1013.3459807657844 L 39.908203124999986 1006.2278746377142 L 40.8583984375 999.1478282581048 L 41.80859375 992.1057387277212 L 42.758789062499986 985.1015032652651 L 43.708984375 978.1350192073745 L 44.659179687500014 971.2061840086249 L 45.609375 964.314895241528 L 46.5595703125 957.4610505965322 L 47.509765625 950.644547882023 L 48.4599609375 943.8652850243221 L 49.41015625 937.1231600676882 L 50.3603515625 930.4180711743168 L 51.310546875 923.7499166243398 L 52.2607421875 917.118594815826 L 53.2109375 910.524004264781 L 54.1611328125 903.9660436051469 L 55.111328125 897.4446115888027 L 56.0615234375 890.959607085564 L 57.01171875 884.5109290831832 L 57.9619140625 878.0984766873493 L 58.912109374999986 871.7221491216881 L 59.86230468749999 865.381845727762 L 60.81249999999999 859.0774659650701 L 61.76269531249999 852.8089094110485 L 62.712890625 846.5760757610697 L 63.66308593749999 840.378864828443 L 64.61328125 834.2171765444145 L 65.5634765625 828.0909109581669 L 66.51367187499999 821.9999682368197 L 67.46386718749999 815.9442486654289 L 68.4140625 809.9236526469874 L 69.3642578125 803.938080702425 L 70.314453125 797.9874334706078 L 71.2646484375 792.0716117083388 L 72.21484375 786.1905162903578 L 73.1650390625 780.3440482093412 L 74.115234375 774.5321085759019 L 75.0654296875 768.7545986185903 L 76.015625 763.0114196838924 L 76.9658203125 757.3024732362317 L 77.91601562499999 751.6276608579682 L 78.8662109375 745.9868842493985 L 79.81640625 740.380045228756 L 80.7666015625 734.807045732211 L 81.716796875 729.26778781387 L 82.66699218749999 723.7621736457768 L 83.6171875 718.2901055179115 L 84.5673828125 712.851485838191 L 85.51757812499999 707.4462171324693 L 86.46777343749999 702.0742020445364 L 87.41796874999999 696.7353433361195 L 88.36816406249999 691.4295438868824 L 89.318359375 686.1567066944257 L 90.2685546875 680.9167348742865 L 91.21875 675.7095316599386 L 92.16894531249999 670.5350004027931 L 93.11914062499999 665.3930445721969 L 94.06933593749999 660.2835677554342 L 95.01953125 655.2064736577258 L 95.9697265625 650.1616661022291 L 96.91992187499999 645.1490490300386 L 97.87011718749999 640.1685265001847 L 98.82031249999999 635.2200026896354 L 99.7705078125 630.3033818932948 L 100.72070312499999 625.4185685240042 L 101.67089843749999 620.565467112541 L 102.62109374999999 615.74398230762 L 103.57128906249999 610.9540188758922 L 104.52148437499999 606.1954817019454 L 105.47167968749999 601.4682757883043 L 106.42187499999999 596.7723062554301 L 107.37207031249999 592.1074783417209 L 108.32226562499999 587.4736974035116 L 109.27246093749999 582.8708689150733 L 110.22265624999999 578.2988984686143 L 111.17285156249999 573.7576917742795 L 112.12304687499999 569.2471546601503 L 113.07324218749999 564.767193072245 L 114.02343749999999 560.3177130745189 L 114.97363281249999 555.8986208488633 L 115.92382812499999 551.5098226951068 L 116.87402343749999 547.1512250310145 L 117.82421874999999 542.8227343922883 L 118.77441406249999 538.5242574325666 L 119.72460937499999 534.2557009234247 L 120.67480468749999 530.0169717543745 L 121.62499999999999 525.8079769328649 L 122.57519531249999 521.6286235842811 L 123.52539062499999 517.4788189519452 L 124.47558593749999 513.3584703971159 L 125.42578124999999 509.2674853989889 L 126.37597656249999 505.2057715546965 L 127.32617187499999 501.17323657930746 L 128.27636718749997 497.1697883058273 L 129.22656249999997 493.19533468519876 L 130.1767578125 489.2497837863008 L 131.12695312499997 485.33304379594887 L 132.07714843749997 481.4450230188957 L 133.02734374999997 477.58562987783057 L 133.97753906249997 473.7547729133793 L 134.92773437499997 469.9523607841046 L 135.87792968749997 466.1783022665055 L 136.82812499999997 462.4325062550185 L 137.77832031249997 458.71488176201603 L 138.728515625 455.02533791780775 L 139.6787109375 451.36378397063953 L 140.62890624999997 447.73012928669465 L 141.57910156249997 444.12428335009247 L 142.52929687499997 440.54615576288944 L 143.47949218749997 436.99565624507846 L 144.42968749999997 433.4726946345893 L 145.37988281249997 429.9771808872883 L 146.33007812499997 426.50902507697884 L 147.28027343749997 423.0681373954006 L 148.23046874999997 419.6544281522302 L 149.18066406249997 416.26780777508094 L 150.13085937499997 412.9081868095029 L 151.0810546875 409.57547591898265 L 152.03124999999997 406.2695858849436 L 152.98144531249997 402.990427606746 L 153.93164062499997 399.73791210168656 L 154.88183593749997 396.511950504999 L 155.83203125 393.3124540698534 L 156.7822265625 390.1393341673569 L 157.732421875 386.992502286553 L 158.68261718749997 383.87187003442205 L 159.63281249999997 380.7773491358815 L 160.5830078125 377.7088514337849 L 161.53320312499997 374.6662888889228 L 162.48339843749997 371.64957358002255 L 163.43359374999997 368.6586177037479 L 164.38378906249997 365.6933335746996 L 165.333984375 362.753633625415 L 166.28417968749997 359.8394304063682 L 167.23437499999997 356.9506365859702 L 168.18457031249997 354.0871649505682 L 169.13476562499997 351.2489284044465 L 170.08496093749997 348.43583996982613 L 171.03515624999997 345.6478127868644 L 171.98535156249997 342.88476011365594 L 172.93554687499997 340.1465953262318 L 173.88574218749997 337.43323191855984 L 174.83593749999997 334.7445835025443 L 175.7861328125 332.08056380802634 L 176.736328125 329.441086682784 L 177.68652343749997 326.8260660925321 L 178.63671874999997 324.2354161209213 L 179.58691406249997 321.6690509695403 L 180.53710937499997 319.1268849579136 L 181.48730468749997 316.60883252350243 L 182.43749999999997 314.1148082217055 L 183.38769531249997 311.644726725857 L 184.33789062499997 309.19850282722905 L 185.28808593749997 306.7760514350298 L 186.23828124999997 304.3772875764041 L 187.18847656249997 302.0021263964338 L 188.13867187499997 299.6504831581375 L 189.08886718749997 297.3222732424698 L 190.03906249999997 295.01741214832305 L 190.98925781249997 292.7358154925256 L 191.93945312499997 290.47739900984277 L 192.88964843749997 288.24207855297675 L 193.83984375 286.0297700925656 L 194.7900390625 283.8403897171854 L 195.740234375 281.673853633348 L 196.69042968749997 279.53007816550223 L 197.64062499999997 277.40897975603366 L 198.5908203125 275.31047496526435 L 199.54101562499997 273.2344804714535 L 200.49121093749997 271.1809130707967 L 201.44140624999997 269.1496896774263 L 202.3916015625 267.1407273234114 L 203.341796875 265.15394315875767 L 204.29199218749997 263.1892544514079 L 205.2421875 261.24657858724106 L 206.1923828125 259.32583307007314 L 207.142578125 257.4269355216569 L 208.0927734375 255.54980368168174 L 209.04296874999997 253.6943554077734 L 209.99316406249997 251.86050867549477 L 210.94335937499997 250.04818157834563 L 211.8935546875 248.25729232776177 L 212.84374999999997 246.48775925311645 L 213.79394531249997 244.73950080171915 L 214.744140625 243.0124355388159 L 215.6943359375 241.30648214759015 L 216.64453125 239.6215594291616 L 217.59472656249997 237.95758630258672 L 218.54492187499997 236.31448180485847 L 219.49511718749994 234.69216509090688 L 220.44531249999997 233.0905554335984 L 221.3955078125 231.50957222373643 L 222.34570312499997 229.9491349700611 L 223.29589843749997 228.40916329924903 L 224.24609374999994 226.88957695591375 L 225.19628906249994 225.39029580260524 L 226.14648437499997 223.91123981981036 L 227.09667968749997 222.45232910595269 L 228.04687499999997 221.01348387739267 L 228.99707031249994 219.59462446842724 L 229.94726562499997 218.19567133129 L 230.8974609375 216.81654503615152 L 231.84765624999997 215.45716627111858 L 232.79785156249997 214.11745584223547 L 233.748046875 212.7973346734824 L 234.6982421875 211.4967238067768 L 235.6484375 210.2155444019727 L 236.59863281249997 208.95371773686054 L 237.548828125 207.7111652071676 L 238.4990234375 206.48780832655825 L 239.44921875 205.28356872663346 L 240.3994140625 204.09836815693052 L 241.34960937499997 202.93212848492362 L 242.29980468749997 201.78477169602377 L 243.24999999999997 200.6562198935785 L 244.2001953125 199.5463952988722 L 245.150390625 198.45522025112632 L 246.10058593749997 197.38261720749813 L 247.05078124999997 196.32850874308235 L 248.00097656249994 195.29281755091029 L 248.95117187499997 194.27546644194956 L 249.9013671875 193.27637834510517 L 250.85156249999997 192.29547630721822 L 251.80175781249997 191.33268349306684 L 252.75195312499997 190.3879231853657 L 253.7021484375 189.4611187847661 L 254.65234374999997 188.5521938098567 L 255.60253906249997 187.66107189716217 L 256.552734375 186.7876768011439 L 257.5029296875 185.93193239420054 L 258.453125 185.09376266666698 L 259.4033203125 184.27309172681476 L 260.353515625 183.4698438008527 L 261.3037109375 182.68394323292557 L 262.25390625 181.91531448511557 L 263.2041015625 181.16388213744108 L 264.154296875 180.42957088785738 L 265.1044921875 179.71230555225634 L 266.0546875 179.0120110644673 L 267.0048828125 178.32861247625488 L 267.955078125 177.66203495732168 L 268.9052734375 177.0122037953064 L 269.85546875 176.37904439578483 L 270.8056640625 175.7624822822687 L 271.755859375 175.16244309620754 L 272.7060546875 174.57885259698674 L 273.65625 174.01163666192872 L 274.6064453125 173.46072128629282 L 275.556640625 172.92603258327426 L 276.5068359375 172.4074967840063 L 277.45703125 171.90504023755784 L 278.4072265625 171.41858941093471 L 279.357421875 170.94807088908 L 280.3076171875 170.4934113748726 L 281.2578125 170.05453768912867 L 282.20800781249994 169.63137677060115 L 283.15820312499994 169.22385567597962 L 284.1083984375 168.8319015798901 L 285.05859375 168.4554417748958 L 286.00878906249994 168.09440367149602 L 286.958984375 167.74871479812725 L 287.9091796875 167.41830280116233 L 288.859375 167.10309544491145 L 289.8095703125 166.80302061162092 L 290.75976562499994 166.51800630147375 L 291.7099609375 166.24798063259016 L 292.66015625 165.9928718410265 L 293.6103515625 165.75260828077603 L 294.560546875 165.52711842376902 L 295.5107421875 165.3163308598722 L 296.4609375 165.120174296889 L 297.4111328125 164.93857756055945 L 298.361328125 164.77146959456036 L 299.3115234375 164.6187794605056 L 300.26171874999994 164.48043633794543 L 301.21191406249994 164.35636952436664 L 302.16210937499994 164.24650843519316 L 303.1123046875 164.15078260378527 L 304.0625 164.06912168144027 L 305.01269531249994 164.00145543739177 L 305.962890625 163.94771375881055 L 306.9130859375 163.90782665080383 L 307.86328125 163.8817242364156 L 308.8134765625 163.86933675662647 L 309.76367187499994 163.8705945703539 L 310.71386718749994 163.88542815445192 L 311.66406249999994 163.91376810371162 L 312.61425781249994 163.9555451308603 L 313.5644531249999 164.01069006656235 L 314.51464843749994 164.07913385941856 L 315.46484374999994 164.1608075759666 L 316.41503906249994 164.25564240068115 L 317.365234375 164.36356963597314 L 318.3154296875 164.48452070219025 L 319.26562499999994 164.618427137617 L 320.21582031249994 164.76522059847468 L 321.16601562499994 164.92483285892126 L 322.1162109375 165.0971958110515 L 323.06640625 165.28224146489652 L 324.01660156249994 165.47990194842453 L 324.966796875 165.69010950754034 L 325.9169921875 165.9127965060851 L 326.8671875 166.14789542583742 L 327.8173828125 166.39533886651213 L 328.76757812499994 166.65505954576054 L 329.7177734375 166.92699029917162 L 330.66796875 167.2110640802698 L 331.6181640625 167.5072139605171 L 332.568359375 167.81537312931164 L 333.5185546875 168.13547489398923 L 334.46875 168.46745267982135 L 335.4189453125 168.81124003001662 L 336.369140625 169.16677060572044 L 337.3193359375 169.5339781860148 L 338.26953125 169.9127966679182 L 339.2197265625 170.30316006638645 L 340.169921875 170.70500251431167 L 341.1201171875 171.11825826252232 L 342.0703125 171.54286167978432 L 343.0205078125 171.97874725279996 L 343.970703125 172.42584958620807 L 344.9208984375 172.88410340258451 L 345.87109375 173.3534435424416 L 346.8212890625 173.83380496422853 L 347.77148437499994 174.325122744331 L 348.7216796875 174.82733207707156 L 349.671875 175.3403682747097 L 350.6220703125 175.86416676744113 L 351.572265625 176.39866310339892 L 352.5224609375 176.94379294865178 L 353.47265625 177.4994920872066 L 354.4228515625 178.06569642100555 L 355.373046875 178.64234196992834 L 356.32324218749994 179.22936487179163 L 357.27343749999994 179.82670138234778 L 358.22363281249994 180.4342878752866 L 359.17382812499994 181.0520608422346 L 360.1240234375 181.67995689275472 L 361.07421874999994 182.31791275434716 L 362.02441406249994 182.96586527244756 L 362.974609375 183.62375141043015 L 363.9248046875 184.2915082496039 L 364.875 184.969072989216 L 365.82519531249994 185.65638294644998 L 366.77539062499994 186.35337555642536 L 367.7255859375 187.0599883721991 L 368.67578125 187.77615906476456 L 369.6259765625 188.5018254230522 L 370.576171875 189.23692535392888 L 371.5263671875 189.98139688219794 L 372.4765625 190.73517815059995 L 373.4267578125 191.49820741981182 L 374.376953125 192.27042306844737 L 375.32714843749994 193.051763593057 L 376.27734374999994 193.84216760812762 L 377.22753906249994 194.64157384608347 L 378.17773437499994 195.4499211572852 L 379.1279296875 196.26714851002987 L 380.07812499999994 197.09319499055152 L 381.02832031249994 197.92799980302084 L 381.978515625 198.77150226954518 L 382.92871093749994 199.62364183016894 L 383.87890624999994 200.48435804287283 L 384.82910156249994 201.35359058357437 L 385.77929687499994 202.23127924612743 L 386.72949218749994 203.11736394232344 L 387.67968749999994 204.0117847018904 L 388.62988281249994 204.91448167249223 L 389.58007812499994 205.82539511973027 L 390.53027343749994 206.7444654271426 L 391.48046874999994 207.67163309620275 L 392.43066406249994 208.60683874632252 L 393.38085937499994 209.55002311485055 L 394.33105468749994 210.50112705707056 L 395.28124999999994 211.46009154620424 L 396.23144531249994 212.42685767340993 L 397.18164062499994 213.40136664778186 L 398.13183593749994 214.38355979635207 L 399.08203124999994 215.37337856408863 L 400.03222656249994 216.37076451389623 L 400.982421875 217.37565932661664 L 401.93261718749994 218.38800480102861 L 402.88281249999994 219.40774285384668 L 403.83300781249994 220.43481551972297 L 404.78320312499994 221.46916495124572 L 405.7333984375 222.51073341894005 L 406.68359374999994 223.55946331126813 L 407.63378906249994 224.61529713462846 L 408.583984375 225.67817751335656 L 409.5341796875 226.74804718972382 L 410.484375 227.8248490239398 L 411.43457031249994 228.9085259941494 L 412.38476562499994 229.99902119643536 L 413.3349609375 231.09627784481597 L 414.28515625 232.20023927124726 L 415.23535156249994 233.3108489256207 L 416.185546875 234.42805037576636 L 417.1357421875 235.55178730744967 L 418.0859375 236.68200352437282 L 419.0361328125 237.81864294817478 L 419.98632812499994 238.9616496184318 L 420.93652343749994 240.1109676926559 L 421.88671874999994 241.26654144629754 L 422.83691406249994 242.42831527274143 L 423.78710937499994 243.5962336833112 L 424.73730468749994 244.77024130726568 L 425.68749999999994 245.95028289180095 L 426.63769531249994 247.13630330205024 L 427.587890625 248.32824752108286 L 428.5380859375 249.52606064990528 L 429.48828124999994 250.7296879074603 L 430.43847656249994 251.93907463062737 L 431.38867187499994 253.15416627422258 L 432.33886718749994 254.37490841100032 L 433.28906249999994 255.60124673164933 L 434.2392578124999 256.83312704479636 L 435.18945312499994 258.0704952770045 L 436.13964843749994 259.31329747277437 L 437.08984375 260.56147979454147 L 438.0400390625 261.8149885226803 L 438.99023437499994 263.0737700555002 L 439.94042968749994 264.3377709092482 L 440.89062499999994 265.60693771810804 L 441.8408203125 266.8812172341993 L 442.79101562499994 268.1605563275791 L 443.7412109374999 269.4449019862418 L 444.69140624999994 270.73420131611704 L 445.64160156249994 272.02840154107173 L 446.591796875 273.32745000291015 L 447.5419921875 274.63129416137224 L 448.49218749999994 275.9398815941353 L 449.44238281249994 277.25315999681357 L 450.39257812499994 278.5710771829574 L 451.3427734375 279.8935810840543 L 452.29296875 281.22061974952805 L 453.24316406250006 282.55214134673963 L 454.193359375 283.8880941609858 L 455.14355468749994 285.22842659550145 L 456.09375 286.57308717145725 L 457.0439453125 287.9220245279612 L 457.99414062499994 289.27518742205643 L 458.94433593749994 290.6325247287249 L 459.89453124999994 291.9939854408841 L 460.8447265625 293.3595186693884 L 461.794921875 294.729073643029 L 462.74511718750006 296.10259970853383 L 463.6953125 297.48004633056667 L 464.64550781249994 298.86136309173 L 465.595703125 300.2464996925611 L 466.5458984375 301.6354059515347 L 467.49609375000006 303.02803180506214 L 468.44628906250006 304.4243273074918 L 469.396484375 305.82424263110806 L 470.3466796875 307.2277280661327 L 471.296875 308.6347340207243 L 472.24707031250006 310.04521102097704 L 473.197265625 311.45910971092303 L 474.14746093749994 312.87638085253127 L 475.09765625 314.29697532570526 L 476.0478515625 315.72084412828883 L 476.99804687499994 317.1479383760583 L 477.94824218749994 318.5782093027302 L 478.89843749999994 320.0116082599566 L 479.8486328125 321.4480867173255 L 480.79882812499994 322.8875962623629 L 481.7490234374999 324.3300886005295 L 482.69921874999994 325.7755155552261 L 483.64941406249994 327.2238290677865 L 484.599609375 328.67498119748336 L 485.5498046875 330.1289241215261 L 486.49999999999994 331.5856101350595 L 487.45019531249994 333.0449916511667 L 488.40039062499994 334.507021200866 L 489.3505859375 335.9716514331135 L 490.30078125 337.4388351148018 L 491.25097656250006 338.90852513076004 L 492.201171875 340.38067448375386 L 493.15136718749994 341.8552362944855 L 494.1015625 343.33216380159536 L 495.0517578125 344.8114103616583 L 496.00195312499994 346.2929294491872 L 496.95214843749994 347.7766746566326 L 497.90234374999994 349.2625996943792 L 498.8525390625 350.750658390751 L 499.80273437499994 352.2408046920066 L 500.7529296874999 353.73299266234267 L 501.70312499999994 355.22717648389255 L 502.65332031249994 356.7233104567257 L 503.6035156249999 358.22134899884827 L 504.5537109374999 359.7212466462035 L 505.5039062499999 361.22295805267106 L 506.45410156249994 362.72643799006863 L 507.40429687499994 364.23164134814743 L 508.3544921875 365.7385231345993 L 509.30468749999994 367.2470384750494 L 510.2548828124999 368.75714261306246 L 511.20507812499994 370.26879091013745 L 512.1552734375 371.7819388457118 L 513.10546875 373.2965420171593 L 514.0556640625 374.81255613978874 L 515.005859375 376.32993704684907 L 515.9560546875 377.84864068952203 L 516.90625 379.3686231369295 L 517.8564453125 380.889840576128 L 518.806640625 382.4122493121107 L 519.7568359374999 383.9358057678092 L 520.70703125 385.46046648408975 L 521.6572265625 386.9861881197566 L 522.607421875 388.51292745155035 L 523.5576171875 390.0406413741484 L 524.5078125 391.56928690016497 L 525.4580078125 393.09882116015 L 526.408203125 394.62920140259206 L 527.3583984375 396.16038499391476 L 528.30859375 397.69232941847883 L 529.2587890625 399.22499227858214 L 530.208984375 400.75833129445897 L 531.1591796875 402.2923043042803 L 532.109375 403.8268692641538 L 533.0595703125 405.3619842481239 L 534.009765625 406.8976074481718 L 534.9599609375 408.43369717421507 L 535.91015625 409.9702118541092 L 536.8603515625 411.5071100336444 L 537.810546875 413.04435037654946 L 538.7607421875 414.58189166448835 L 539.7109375 416.11969279706244 L 540.6611328125 417.65771279181126 L 541.611328125 419.1959107842081 L 542.5615234375 420.73424602766505 L 543.51171875 422.2726778935301 L 544.4619140625 423.81116587108943 L 545.412109375 425.34966956756296 L 546.3623046875 426.88814870810984 L 547.3125 428.4265631358253 L 548.2626953125 429.9648728117412 L 549.212890625 431.50303781482586 L 550.1630859375 433.04101834198485 L 551.11328125 434.57877470805965 L 552.0634765625 436.11626734582865 L 553.013671875 437.6534568060087 L 553.9638671875 439.1903037572504 L 554.9140625 440.7267689861428 L 555.8642578125 442.26281339721095 L 556.814453125 443.79839801291837 L 557.7646484375 445.3334839736633 L 558.71484375 446.8680325377813 L 559.6650390625 448.4020050815449 L 560.615234375 449.93536309916306 L 561.5654296875 451.46806820278175 L 562.515625 453.0000821224827 L 563.4658203125 454.5313667062852 L 564.416015625 456.0618839201455 L 565.3662109375 457.5915958479573 L 566.31640625 459.1204646915482 L 567.2666015625 460.64845277068457 L 568.216796875 462.17552252306984 L 569.1669921875 463.70163650434296 L 570.1171875 465.22675738808033 L 571.0673828125 466.75084796579466 L 572.017578125 468.27387114693556 L 572.9677734374999 469.7957899588884 L 573.91796875 471.31656754697843 L 574.8681640625 472.83616717446336 L 575.818359375 474.35455222254086 L 576.7685546875 475.87168619034253 L 577.71875 477.38753269493924 L 578.6689453125 478.90205547133786 L 579.619140625 480.41521837248155 L 580.5693359375 481.92698536924934 L 581.51953125 483.4373205504595 L 582.4697265625 484.9461881228634 L 583.419921875 486.45355241115254 L 584.3701171875 487.95937785795377 L 585.3203125 489.46362902383026 L 586.2705078125 490.9662705872825 L 587.220703125 492.46726734474686 L 588.1708984375 493.96658421059686 L 589.12109375 495.46418621714355 L 590.0712890625 496.96003851463456 L 591.021484375 498.45410637125264 L 591.9716796874999 499.94635517311826 L 592.921875 501.43675042428964 L 593.8720703125 502.9252577467596 L 594.822265625 504.41184288045935 L 595.7724609374999 505.8964716832558 L 596.7226562499999 507.3791101309533 L 597.6728515625 508.8597243172942 L 598.623046875 510.3382804539528 L 599.5732421875 511.8147448705454 L 600.5234375 513.2890840146226 L 601.4736328124999 514.7612644516719 L 602.423828125 516.2312528651169 L 603.3740234375 517.6990160563196 L 604.32421875 519.1645209445778 L 605.2744140625 520.6277345671252 L 606.224609375 522.088624079134 L 607.1748046875 523.5471567537113 L 608.125 525.0032999819013 L 609.0751953125 526.4570212726865 L 610.025390625 527.9082882529832 L 610.9755859374999 529.3570686676476 L 611.92578125 530.8033303794715 L 612.8759765625 532.2470413691815 L 613.826171875 533.6881697354439 L 614.7763671875 535.1266836948583 L 615.7265625 536.5625515819652 L 616.6767578125 537.9957418492384 L 617.626953125 539.4262230670896 L 618.5771484375 540.8539639238684 L 619.52734375 542.278933225858 L 620.4775390625 543.7010998972819 L 621.427734375 545.1204329802974 L 622.3779296875 546.5369016349997 L 623.328125 547.9504751394225 L 624.2783203125 549.361122889532 L 625.228515625 550.7688143992353 L 626.1787109375 552.1735193003744 L 627.12890625 553.5752073427274 L 628.0791015625 554.9738483940105 L 629.029296875 556.369412439876 L 629.9794921874999 557.7618695839117 L 630.9296875 559.1511900476444 L 631.8798828125 560.5373441705365 L 632.830078125 561.9203024099849 L 633.7802734374999 563.300035341329 L 634.7304687499999 564.6765136578383 L 635.6806640624999 566.0497081707238 L 636.630859375 567.4195898091309 L 637.5810546875 568.7861296201411 L 638.53125 570.1492987687748 L 639.4814453124999 571.5090685379881 L 640.4316406249999 572.8654103286735 L 641.3818359375 574.2182956596612 L 642.33203125 575.567696167716 L 643.2822265625 576.9135836075419 L 644.232421875 578.2559298517774 L 645.1826171874999 579.5947068909995 L 646.1328125 580.9298868337214 L 647.0830078125 582.2614419063929 L 648.033203125 583.5893444533999 L 648.9833984374999 584.9135669370669 L 649.9335937499999 586.2340819376511 L 650.8837890625 587.5508621533518 L 651.8339843749999 588.8638804003008 L 652.7841796874999 590.1731096125683 L 653.7343749999999 591.4785228421613 L 654.6845703124999 592.7800932590228 L 655.6347656249999 594.0777941510337 L 656.5849609374999 595.37159892401 L 657.5351562499999 596.6614811017066 L 658.4853515624999 597.9474143258111 L 659.4355468749999 599.2293723559526 L 660.3857421875 600.5073290696948 L 661.3359374999999 601.7812584625374 L 662.2861328124999 603.0511346479175 L 663.2363281249999 604.3169318572093 L 664.1865234374999 605.5786244397232 L 665.13671875 606.8361868627053 L 666.0869140625 608.0895937113414 L 667.037109375 609.3388196887529 L 667.9873046874999 610.5838396159934 L 668.9374999999999 611.8246284320602 L 669.8876953125 613.0611611938825 L 670.8378906249999 614.2934130763292 L 671.7880859374999 615.5213593722035 L 672.7382812499999 616.7449754922461 L 673.6884765624999 617.9642369651347 L 674.638671875 619.1791194374846 L 675.5888671875 620.3895986738476 L 676.5390625 621.5956505567087 L 677.4892578124999 622.7972510864934 L 678.4394531249999 623.9943763815633 L 679.3896484375 625.1870026782174 L 680.33984375 626.3751063306877 L 681.2900390625 627.5586638111479 L 682.240234375 628.7376517097047 L 683.1904296874999 629.9120467344039 L 684.140625 631.0818257112264 L 685.0908203125 632.24696558409 L 686.041015625 633.4074434148495 L 686.9912109374999 634.5632363832965 L 687.9414062499999 635.7143217871607 L 688.8916015625 636.8606770421054 L 689.8417968749999 638.0022796817333 L 690.7919921874999 639.1391073575817 L 691.7421874999999 640.2711378391276 L 692.6923828124999 641.3983490137816 L 693.6425781249999 642.5207188868922 L 694.5927734374999 643.6382255817445 L 695.5429687499999 644.7508473395612 L 696.4931640624999 645.8585625195002 L 697.4433593749999 646.9613495986578 L 698.3935546875 648.0591871720657 L 699.3437499999999 649.152053952693 L 700.2939453124999 650.2399287714443 L 701.2441406249999 651.3227905771627 L 702.1943359374999 652.400618436627 L 703.14453125 653.4733915345533 L 704.0947265625 654.5410891735924 L 705.0449218749999 655.6036907743343 L 705.9951171874999 656.6611758753058 L 706.9453124999999 657.7135241329685 L 707.8955078125 658.7607153217218 L 708.8457031249999 659.8027293339 L 709.7958984374999 660.8395461797795 L 710.7460937499999 661.8711459875658 L 711.6962890624999 662.8975090034075 L 712.6464843749999 663.9186155913862 L 713.5966796874999 664.934446233522 L 714.5468749999999 665.9449815297696 L 715.4970703124999 666.9502021980231 L 716.4472656249999 667.9500890741133 L 717.3974609374998 668.9446231118039 L 718.3476562499999 669.9337853828005 L 719.2978515624999 670.9175570767411 L 720.2480468749999 671.8959195012023 L 721.1982421874999 672.8688540816983 L 722.1484374999999 673.836342361677 L 723.0986328124999 674.7983660025284 L 724.0488281249999 675.7549067835735 L 724.9990234374999 676.7059466020718 L 725.9492187499999 677.65146747322 L 726.8994140625 678.5914515301539 L 727.8496093749999 679.5258810239413 L 728.7998046874999 680.4547383235898 L 729.7499999999999 681.3780059160432 L 730.7001953124999 682.2956664061824 L 731.6503906249999 683.2077025168221 L 732.6005859374999 684.1140970887182 L 733.5507812499999 685.0148330805599 L 734.5009765624999 685.9098935689749 L 735.4511718749999 686.799261748529 L 736.4013671875 687.6829209317182 L 737.3515624999999 688.5608545489821 L 738.3017578124999 689.4330461486959 L 739.2519531249999 690.2994793971693 L 740.2021484374999 691.1601380786492 L 741.15234375 692.0150060953194 L 742.1025390625 692.8640674673032 L 743.0527343749999 693.7073063326552 L 744.0029296874999 694.5447069473689 L 744.9531249999999 695.3762536853803 L 745.9033203125 696.2019310385515 L 746.853515625 697.0217236166891 L 747.8037109374999 697.8356161475348 L 748.7539062499999 698.6435934767667 L 749.7041015624999 699.4456405679987 L 750.6542968749998 700.2417425027802 L 751.6044921874999 701.0318844806004 L 752.5546874999999 701.8160518188851 L 753.5048828124999 702.5942299529944 L 754.4550781249999 703.3664044362271 L 755.4052734374998 704.1325609398182 L 756.3554687499999 704.8926852529372 L 757.3056640624999 705.6467632826933 L 758.2558593749998 706.3947810541313 L 759.2060546874998 707.1367247102344 L 760.1562499999998 707.8725805119196 L 761.1064453124999 708.602334838042 L 762.0566406249999 709.3259741853919 L 763.0068359374998 710.0434851687007 L 763.9570312499998 710.7548545206306 L 764.9072265624998 711.4600690917866 L 765.8574218749997 712.1591158507032 L 766.8076171874998 712.8519818838613 L 767.7578124999998 713.5386543956677 L 768.7080078124998 714.2191207084718 L 769.6582031249998 714.8933682625631 L 770.6083984374999 715.5613846161574 L 771.5585937499999 716.2231574454199 L 772.5087890624999 716.8786745444438 L 773.4589843749999 717.5279238252579 L 774.4091796874998 718.170893317836 L 775.3593749999999 718.8075711700819 L 776.3095703124999 719.437945647837 L 777.2597656249998 720.0620051348822 L 778.2099609374998 720.6797381329334 L 779.1601562499998 721.2911332616404 L 780.1103515624999 721.8961792585956 L 781.0605468749999 722.4948649793224 L 782.0107421874999 723.0871793972863 L 782.9609374999999 723.6731116038843 L 783.9111328125 724.2526508084527 L 784.861328125 724.8257863382667 L 785.8115234374999 725.3925076385322 L 786.7617187499999 725.9528042723979 L 787.7119140624999 726.5066659209457 L 788.6621093749998 727.0540823831951 L 789.6123046874999 727.5950435761022 L 790.5624999999999 728.129539534563 L 791.5126953124999 728.657560411403 L 792.4628906249999 729.1790964773915 L 793.4130859374998 729.6941381212324 L 794.3632812499999 730.2026758495613 L 795.3134765624999 730.704700286959 L 796.2636718749998 731.2002021759373 L 797.2138671874998 731.6891723769465 L 798.1640624999998 732.1716018683717 L 799.1142578124999 732.6474817465396 L 800.0644531249999 733.1168032257076 L 801.0146484374999 733.579557638074 L 801.9648437499999 734.0357364337717 L 802.9150390625 734.4853311808711 L 803.865234375 734.9283335653798 L 804.8154296874999 735.3647353912412 L 805.7656249999999 735.794528580336 L 806.7158203124999 736.2177051724801 L 807.6660156249998 736.6342573254268 L 808.6162109374999 737.0441773148716 L 809.5664062499999 737.4474575344341 L 810.5166015624999 737.8440904956864 L 811.4667968749999 738.2340688281232 L 812.4169921875 738.6173852791842 L 813.3671875 738.9940327142431 L 814.3173828125 739.3640041166107 L 815.267578125 739.7272925875345 L 816.2177734374999 740.0838913461989 L 817.16796875 740.4337937297266 L 818.1181640625 740.77699319317 L 819.0683593749999 741.1134833095307 L 820.0185546874999 741.4432577697339 L 820.9687499999999 741.7663103826512 L 821.9189453125 742.0826350750842 L 822.869140625 742.3922258917767 L 823.8193359374999 742.6950769954057 L 824.7695312499999 742.9911826665818 L 825.7197265624999 743.280537303865 L 826.6699218749998 743.5631354237357 L 827.6201171874999 743.8389716606221 L 828.5703124999999 744.1080407668856 L 829.5205078124999 744.3703376128235 L 830.4707031249999 744.6258571866705 L 831.4208984374999 744.8745945945977 L 832.37109375 745.116545060717 L 833.3212890625 745.3517039270714 L 834.271484375 745.5800666536392 L 835.2216796874999 745.8016288183425 L 836.1718749999999 746.0163861170371 L 837.1220703125 746.2243343635129 L 838.0722656249999 746.4254694895003 L 839.0224609374999 746.6197875446622 L 839.9726562499999 746.8072846966019 L 840.9228515624999 746.9879572308587 L 841.873046875 747.1618015509064 L 842.8232421875 747.3288141781587 L 843.7734375 747.4889917519655 L 844.7236328125 747.6423310296092 L 845.6738281250001 747.7888288863159 L 846.6240234375 747.9284823152398 L 847.57421875 748.0612884274798 L 848.5244140625 748.1872444520712 L 849.4746093749999 748.3063477359764 L 850.4248046874999 748.4185957441048 L 851.375 748.5239860592984 L 852.3251953125 748.622516382339 L 853.275390625 748.7141845319372 L 854.2255859374999 748.7989884447489 L 855.1757812499999 748.8769261753641 L 856.1259765625 748.9479958963097 L 857.0761718749999 749.012195898046 L 858.0263671874999 749.0695245889744 L 858.9765624999999 749.119980495429 L 859.9267578124999 749.163562261683 L 860.876953125 749.200268649949 L 861.8271484375 749.2300985403693 L 862.77734375 749.2530509310325 L 863.7275390625 749.269124937951 L 864.6777343750001 749.2783197950885 L 865.6279296875 749.2806348543336 L 866.578125 749.2760695855159 L 867.5283203125 749.2646235764055 L 868.4785156249999 749.2462965327057 L 869.4287109374999 749.2210882780537 L 870.37890625 749.1889987540249 L 871.3291015625 749.1500280201369 L 872.279296875 749.1041762538392 L 873.2294921875 749.0514437505153 L 874.1796875000001 748.9918309234938 L 875.1298828125001 748.9253383040309 L 876.0800781250001 748.851966541327 L 877.0302734375 748.7717164025106 L 877.98046875 748.6845887726575 L 878.9306640625001 748.590584654775 L 879.880859375 748.4897051698013 L 880.8310546875 748.3819515566232 L 881.78125 748.2673251720537 L 882.7314453125 748.1458274908465 L 883.6816406250001 748.0174601056998 L 884.6318359375 747.8822247272318 L 885.58203125 747.7401231840107 L 886.5322265625 747.5911574225375 L 887.4824218749999 747.4353295072488 L 888.4326171874999 747.2726416205193 L 889.3828125 747.1030960626597 L 890.3330078125 746.9266952519183 L 891.283203125 746.7434417244785 L 892.2333984374999 746.5533381344634 L 893.1835937499999 746.3563872539298 L 894.1337890625 746.1525919728692 L 895.0839843749999 745.9419552992189 L 896.0341796874999 745.7244803588403 L 896.9843749999999 745.500170395542 L 897.9345703124999 745.2690287710677 L 898.884765625 745.0310589650882 L 899.8349609374999 744.7862645752248 L 900.7851562499999 744.5346493170271 L 901.7353515624999 744.2762170239818 L 902.6855468749998 744.010971647517 L 903.6357421874998 743.7389172569892 L 904.5859374999999 743.4600580396996 L 905.5361328124999 743.1743983008887 L 906.4863281249999 742.8819424637189 L 907.4365234374999 742.5826950693036 L 908.38671875 742.2766607766882 L 909.3369140625 741.9638443628514 L 910.287109375 741.6442507227163 L 911.2373046874999 741.3178848691348 L 912.1874999999999 740.984751932901 L 913.1376953125 740.6448571627435 L 914.0878906249999 740.2982059253242 L 915.0380859374999 739.9448037052512 L 915.9882812499999 739.5846561050582 L 916.9384765624999 739.2177688452241 L 917.888671875 738.8441477641584 L 918.8388671875 738.4637988182137 L 919.7890625 738.0767280816706 L 920.7392578125 737.6829417467604 L 921.6894531250001 737.2824461236332 L 922.6396484375 736.8752476403863 L 923.58984375 736.4613528430558 L 924.5400390625 736.0407683956098 L 925.4902343749999 735.6135010799527 L 926.4404296874999 735.1795577959294 L 927.390625 734.7389455613173 L 928.3408203125 734.2916715118336 L 929.291015625 733.8377429011306 L 930.2412109374999 733.3771671007997 L 931.1914062499999 732.9099516003647 L 932.1416015625 732.4361040072886 L 933.0917968749999 731.955632046973 L 934.0419921874999 731.468543562754 L 934.9921874999999 730.9748465159015 L 935.9423828124999 730.474548985631 L 936.892578125 729.9676591690825 L 937.8427734374999 729.4541853813441 L 938.7929687499999 728.9341360554351 L 939.7431640624999 728.4075197423081 L 940.6933593749998 727.8743451108616 L 941.6435546874998 727.3346209479239 L 942.5937499999999 726.7883561582598 L 943.5439453124999 726.2355597645774 L 944.4941406249999 725.676240907512 L 945.4443359374998 725.1104088456425 L 946.3945312499998 724.5380729554832 L 947.3447265624999 723.9592427314838 L 948.2949218749998 723.3739277860296 L 949.2451171874998 722.7821378494482 L 950.1953124999998 722.1838827699975 L 951.1455078124998 721.5791725138744 L 952.0957031249999 720.9680171652112 L 953.0458984374999 720.3504269260835 L 953.9960937499999 719.7264121164962 L 954.9462890624999 719.095983174394 L 955.896484375 718.4591506556553 L 956.8466796874999 717.8159252340961 L 957.7968749999999 717.1663177014784 L 958.7470703124999 716.5103389674848 L 959.6972656249998 715.8480000597453 L 960.6474609374998 715.1793121238254 L 961.5976562499999 714.504286423229 L 962.5478515624999 713.8229343393887 L 963.4980468749999 713.1352673716799 L 964.4482421874999 712.4412971374153 L 965.3984375 711.7410353718401 L 966.3486328125 711.0344939281426 L 967.298828125 710.3216847774403 L 968.2490234374999 709.6026200087942 L 969.1992187499999 708.8773118291981 L 970.1494140625 708.1457725635823 L 971.0996093749999 707.4080146548172 L 972.0498046874999 706.6640506637071 L 972.9999999999999 705.9138932689901 L 973.9501953124999 705.157555267346 L 974.900390625 704.3950495733906 L 975.8505859374999 703.6263892196805 L 976.8007812499999 702.8515873566924 L 977.7509765624999 702.0706572528626 L 978.7011718749998 701.283612294548 L 979.6513671874998 700.4904659860458 L 980.6015624999999 699.691231949595 L 981.5517578124999 698.8859239253642 L 982.5019531249999 698.0745557714636 L 983.4521484374999 697.2571414639373 L 984.40234375 696.4336950967696 L 985.3525390625 695.6042308818791 L 986.302734375 694.7687631491171 L 987.2529296874999 693.9273063462803 L 988.2031249999999 693.0798750390982 L 989.1533203125 692.2264839112306 L 990.1035156249999 691.367147764284 L 991.0537109374999 690.5018815178001 L 992.0039062499999 689.6307002092476 L 992.9541015624999 688.7536189940434 L 993.904296875 687.8706531455407 L 994.8544921875 686.9818180550176 L 995.8046875 686.0871292317017 L 996.7548828125 685.1866023027475 L 997.7050781250001 684.2802530132531 L 998.6552734375 683.3680972262551 L 999.60546875 682.4501509227218 L 1000.5556640625 681.5264302015521 L 1001.5058593749999 680.5969512795956 L 1002.4560546874999 679.6617304916344 L 1003.40625 678.7207842903744 L 1004.3564453125 677.7741292464842 L 1005.306640625 676.8217820485332 L 1006.2568359374999 675.8637595030682 L 1007.2070312499999 674.9000785345409 L 1008.1572265625 673.9307561853497 L 1009.1074218749999 672.9558096158361 L 1010.0576171874999 671.9752561042753 L 1011.0078124999999 670.9891130468714 L 1011.9580078124999 669.9973979577709 L 1012.908203125 669.0001284690603 L 1013.8583984374999 667.9973223307613 L 1014.8085937499999 666.9889974108337 L 1015.7587890624999 665.9751716951564 L 1016.7089843749998 664.9558632875782 L 1017.6591796874998 663.9310904098475 L 1018.6093749999999 662.900871401688 L 1019.5595703124999 661.8652247207187 L 1020.5097656249999 660.8241689425345 L 1021.4599609374998 659.7777227606408 L 1022.4101562499998 658.7259049864911 L 1023.3603515624999 657.6687345494659 L 1024.3105468749998 656.6062304968983 L 1025.2607421874998 655.5384119940433 L 1026.2109374999998 654.4652983240973 L 1027.1611328124998 653.3869088882002 L 1028.111328125 652.3032632054203 L 1029.0615234375 651.2143809127598 L 1030.01171875 650.1202817651673 L 1030.9619140625 649.0209856355286 L 1031.912109375 647.916512514651 L 1032.8623046875 646.8068825112927 L 1033.8125 645.6921158521513 L 1034.7626953125 644.5722328818467 L 1035.7128906249998 643.4472540629461 L 1036.6630859374998 642.3171999759488 L 1037.61328125 641.1820913192987 L 1038.5634765625 640.041948909364 L 1039.513671875 638.8967936804552 L 1040.4638671875 637.746646684828 L 1041.4140625 636.5915290926572 L 1042.3642578125 635.4314621920701 L 1043.314453125 634.2664673891237 L 1044.2646484375 633.0965662078131 L 1045.21484375 631.9217802900707 L 1046.1650390625 630.7421313957602 L 1047.115234375 629.5576414026946 L 1048.0654296875 628.3683323066126 L 1049.015625 627.1742262211876 L 1049.9658203125 625.9753453780362 L 1050.916015625 624.7717121267149 L 1051.8662109375 623.5633489347119 L 1052.81640625 622.3502783874461 L 1053.7666015625 621.132523188285 L 1054.7167968749998 619.910106158527 L 1055.6669921874998 618.683050237403 L 1056.6171875 617.4513784820898 L 1057.5673828125 616.2151140676962 L 1058.517578125 614.9742802872614 L 1059.4677734374998 613.728900551774 L 1060.4179687499998 612.4789983901545 L 1061.3681640625 611.2245974492537 L 1062.3183593749998 609.965721493865 L 1063.2685546874998 608.7023944067145 L 1064.2187499999998 607.4346401884782 L 1065.1689453124998 606.162482957744 L 1066.119140625 604.8859469510635 L 1067.0693359374998 603.6050565229089 L 1068.0195312499998 602.3198361456887 L 1068.9697265624998 601.0303104097584 L 1069.9199218749995 599.736504023399 L 1070.8701171874995 598.4384418128355 L 1071.8203124999998 597.1361487222275 L 1072.7705078124998 595.8296498136662 L 1073.7207031249998 594.5189702671939 L 1074.6708984374998 593.2041353807747 L 1075.62109375 591.8851705703141 L 1076.5712890625 590.5621013696585 L 1077.521484375 589.2349534305802 L 1078.4716796874998 587.903752522807 L 1079.4218749999998 586.5685245339826 L 1080.3720703125 585.2292954697002 L 1081.3222656249998 583.8860914534869 L 1082.2724609374998 582.5389387268067 L 1083.2226562499998 581.1878636490576 L 1084.1728515624998 579.8328926975778 L 1085.123046875 578.474052467639 L 1086.0732421875 577.1113696724541 L 1087.0234375 575.7448711431621 L 1087.9736328125 574.3745838288596 L 1088.923828125 573.0005347965542 L 1089.8740234375 571.6227512312093 L 1090.82421875 570.2412604357211 L 1091.7744140625 568.8560898309138 L 1092.7246093749998 567.467266955558 L 1093.6748046874998 566.0748194663572 L 1094.625 564.678775137948 L 1095.5751953125 563.2791618629107 L 1096.525390625 561.8760076517615 L 1097.4755859374998 560.4693406329527 L 1098.4257812499998 559.0591890528633 L 1099.3759765625 557.6455812758237 L 1100.3261718749998 556.2285457840933 L 1101.2763671874998 554.8081111778672 L 1102.2265624999998 553.3843061752855 L 1103.1767578124998 551.9571596124099 L 1104.126953125 550.5267004432571 L 1105.0771484375 549.0929577397701 L 1106.02734375 547.6559606918224 L 1106.9775390625 546.2157386072408 L 1107.927734375 544.7723209117689 L 1108.8779296875 543.325737149115 L 1109.828125 541.8760169808918 L 1110.7783203125 540.4231901866644 L 1111.7285156249998 538.967286663941 L 1112.6787109374998 537.5083364281641 L 1113.62890625 536.0463696126924 L 1114.5791015625 534.5814164688504 L 1115.529296875 533.1135073658835 L 1116.4794921875 531.6426727909725 L 1117.4296875 530.1689433492436 L 1118.3798828125 528.6923497637531 L 1119.330078125 527.2129228754998 L 1120.2802734375 525.7306936434022 L 1121.23046875 524.2456931443469 L 1122.1806640625 522.7579525731278 L 1123.130859375 521.2675032424843 L 1124.0810546875 519.774376583106 L 1125.03125 518.2786041436004 L 1125.9814453125 516.7802175905224 L 1126.931640625 515.2792487083548 L 1127.8818359375 513.7757293995317 L 1128.83203125 512.2696916844118 L 1129.7822265625 510.7611677012894 L 1130.7324218749998 509.25018970640605 L 1131.6826171874998 507.7367900739355 L 1132.6328124999998 506.2210012959758 L 1133.5830078125 504.702855982585 L 1134.533203125 503.18238686173544 L 1135.4833984375 501.65962677935556 L 1136.43359375 500.1346086992907 L 1137.3837890625 498.6073657033448 L 1138.333984375 497.07793099124365 L 1139.2841796875 495.5463378806427 L 1140.234375 494.01261980715594 L 1141.1845703125 492.4768103243218 L 1142.1347656249998 490.93894310361213 L 1143.0849609375 489.3990519344396 L 1144.03515625 487.85717072415906 L 1144.9853515625 486.3133334980511 L 1145.935546875 484.76757439934363 L 1146.8857421875 483.21992768919137 L 1147.8359375 481.6704277466964 L 1148.7861328125 480.1191090688815 L 1149.736328125 478.5660062707267 L 1150.6865234375 477.0111540851353 L 1151.63671875 475.45458736294256 L 1152.5869140625 473.89634107294 L 1153.537109375 472.33645030184465 L 1154.4873046875 470.774950254302 L 1155.4375 469.2118762529033 L 1156.3876953125 467.64726373817723 L 1157.337890625 466.0811482685842 L 1158.2880859375 464.5135655205344 L 1159.23828125 462.94455128835654 L 1160.1884765625 461.374141484321 L 1161.138671875 459.80237213863813 L 1162.0888671875 458.22927939946914 L 1163.0390625 456.65489953287965 L 1163.9892578125 455.07926892290004 L 1164.939453125 453.5024240714814 L 1165.8896484375 451.92440159853095 L 1166.83984375 450.3452382418551 L 1167.7900390625 448.7649708572504 L 1168.740234375 447.18363641839244 L 1169.6904296875 445.60127201694564 L 1170.640625 444.01791486247373 L 1171.5908203125 442.43360228249145 L 1172.541015625 440.8483717224544 L 1173.4912109375 439.2622607457476 L 1174.44140625 437.67530703369596 L 1175.3916015625 436.08754838556126 L 1176.341796875 434.49902271853756 L 1177.2919921875 432.90976806776087 L 1178.2421875 431.31982258630325 L 1179.1923828125 429.7292245451737 L 1180.142578125 428.1380123333133 L 1181.0927734375 426.546224457608 L 1182.04296875 424.95389954286804 L 1182.9931640625 423.3610763318573 L 1183.943359375 421.76779368525524 L 1184.8935546875 420.17409058170995 L 1185.84375 418.58000611776515 L 1186.7939453125 416.98557950793304 L 1187.744140625 415.39085008464286 L 1188.6943359375 413.79585729828364 L 1189.64453125 412.20064071715376 L 1190.5947265625 410.60524002751015 L 1191.544921875 409.0096950335342 L 1192.4951171875 407.41404565734706 L 1193.4453125 405.81833193900684 L 1194.3955078125 404.22259403651015 L 1195.345703125 402.6268722257944 L 1196.2958984375 401.0312069007178 L 1197.24609375 399.435638573092 L 1198.1962890625 397.8402078726557 L 1199.146484375 396.24495554708466 L 1200.0966796875 394.6499224620045 L 1201.046875 393.05514960096014 L 1201.9970703125 391.4606780654413 L 1202.947265625 389.8665490748722 L 1203.8974609375 388.2728039666192 L 1204.84765625 386.6794841959847 L 1205.7978515625 385.0866313361878 L 1206.7480468749995 383.49428707841633 L 1207.6982421875 381.90249323177386 L 1208.6484375 380.3112917233123 L 1209.5986328125 378.7207245980044 L 1210.548828125 377.1308340187737 L 1211.4990234375 375.5416622664761 L 1212.44921875 373.9532517399019 L 1213.3994140625 372.3656449557898 L 1214.349609375 370.7788845487956 L 1215.2998046875 369.1930132715235 L 1216.25 367.6080739945185 L 1217.2001953125 366.0241097062515 L 1218.150390625 364.44116351314057 L 1219.1005859375 362.85927863952696 L 1220.05078125 361.27849842770297 L 1221.0009765625 359.6988663378916 L 1221.951171875 358.1204259482506 L 1222.9013671875 356.54322095487976 L 1223.8515625 354.96729517181086 L 1224.8017578125 353.3926925310093 L 1225.751953125 351.8194570823937 L 1226.7021484375 350.2476329937796 L 1227.65234375 348.6772645509851 L 1228.6025390625 347.10839615770374 L 1229.552734375 345.5410723355925 L 1230.5029296875 343.9753377242407 L 1231.453125 342.411237081182 L 1232.4033203125 340.84881528186224 L 1233.353515625 339.28811731970825 L 1234.3037109375 337.72918830603635 L 1235.25390625 336.17207347012743 L 1236.2041015625 334.6168181591896 L 1237.154296875 333.0634678383743 L 1238.1044921875 331.51206809076496 L 1239.0546875 329.96266461738105 L 1240.0048828125 328.41530323717154 L 1240.955078125 326.87002988704626 L 1241.9052734375 325.32689062181964 L 1242.85546875 323.78593161427966 L 1243.8056640625 322.2471991551047 L 1244.7558593749995 320.7107396529469 L 1245.7060546875 319.1765996343905 L 1246.65625 317.64482574394685 L 1247.6064453125 316.1154647440578 L 1248.556640625 314.58856351512895 L 1249.5068359374995 313.06416905545643 L 1250.45703125 311.5423284813353 L 1251.4072265625 310.0230890269396 L 1252.3574218749995 308.5064980444082 L 1253.3076171874995 306.9926030038122 L 1254.2578124999995 305.4814514931709 L 1255.2080078125 303.97309121841454 L 1256.158203125 302.467570003433 L 1257.1083984375 300.9649357900381 L 1258.05859375 299.46523663798655 L 1259.0087890625 297.9685207249745 L 1259.958984375 296.4748363466225 L 1260.9091796875 294.98423191650613 L 1261.859375 293.4967559661178 L 1262.8095703125 292.0124571448971 L 1263.7597656249995 290.531384220217 L 1264.7099609375 289.05358607740254 L 1265.66015625 287.5791117196808 L 1266.6103515625 286.10801026825493 L 1267.560546875 284.64033096224 L 1268.5107421875 283.17612315869326 L 1269.4609375 281.7154363326166 L 1270.4111328125 280.2583200769276 L 1271.361328125 278.8048241025124 L 1272.3115234375 277.3549982381604 L 1273.26171875 275.908892430632 L 1274.2119140625 274.466556744587 L 1275.162109375 273.02804136265615 L 1276.1123046875 271.5933965853835 L 1277.0625 270.16267283125524 L 1278.0126953125 268.73592063670867 L 1278.962890625 267.31319065609637 L 1279.9130859375 265.8945336617187 L 1280.86328125 264.4800005438126 L 1281.8134765625 263.06964231054747 L 1282.7636718749995 261.6635100880395 L 1283.7138671875 260.2616551203323 L 1284.6640625 258.8641287694127 L 1285.6142578125 257.4709825151833 L 1286.564453125 256.0822679555265 L 1287.5146484375 254.69803680620907 L 1288.46484375 253.31834090097266 L 1289.4150390625 251.94323219148077 L 1290.365234375 250.57276274734681 L 1291.3154296875 249.20698475609595 L 1292.265625 247.8459505232106 L 1293.2158203125 246.4897124721042 L 1294.166015625 245.13832314411957 L 1295.1162109375 243.79183519855803 L 1296.06640625 242.4503014126342 L 1297.0166015625 241.11377468150363 L 1297.966796875 239.78230801827124 L 1298.9169921875 238.45595455395937 L 1299.8671875 237.1347675375473 L 1300.8173828125 235.81880033594155 L 1301.767578125 234.5081064339829 L 1302.7177734375 233.20273943445727 L 1303.66796875 231.90275305806972 L 1304.6181640625 230.6082011434852 L 1305.568359375 229.31913764728301 L 1306.5185546875 228.0356166439999 L 1307.46875 226.75769232610207 L 1308.4189453125 225.48541900397765 L 1309.369140625 224.21885110596713 L 1310.3193359375 222.9580431783479 L 1311.26953125 221.70304988533474 L 1312.2197265625 220.45392600907428 L 1313.169921875 219.21072644963783 L 1314.1201171875 217.97350622506144 L 1315.0703125 216.74232047129044 L 1316.0205078125 215.51722444222526 L 1316.970703125 214.29827350969538 L 1317.9208984375 213.08552316346777 L 1318.87109375 211.87902901125403 L 1319.8212890625 210.67884677868267 L 1320.771484375 209.48503230933431 L 1321.7216796875 208.29764156472936 L 1322.671875 207.1167306243201 L 1323.6220703125 205.94235568548618 L 1324.572265625 204.77457306356166 L 1325.5224609375 203.61343919180035 L 1326.47265625 202.45901062139296 L 1327.4228515625 201.31134402149007 L 1328.373046875 200.17049617915416 L 1329.3232421875 199.03652399939483 L 1330.2734375 197.90948450516407 L 1331.2236328125 196.78943483733065 L 1332.173828125 195.67643225472307 L 1333.1240234375 194.57053413408687 L 1334.07421875 193.47179797012484 L 1335.0244140625 192.38028137545177 L 1335.974609375 191.2960420806445 L 1336.9248046875 190.2191379341972 L 1337.875 189.14962690255607 L 1338.8251953125 188.0875670700891 L 1339.775390625 187.0330166391119 L 1340.7255859375 185.98603392987184 L 1341.67578125 184.9466773805509 L 1342.6259765625 183.9150055472785 L 1343.576171875 182.89107710410826 L 1344.5263671875 181.8749508430285 L 1345.4765625 180.8666856739925 L 1346.4267578125 179.86634062485257 L 1347.376953125 178.87397484141366 L 1348.3271484375 177.8896475874276 L 1349.27734375 176.91341824456572 L 1350.2275390625 175.94534631244153 L 1351.177734375 174.98549140861837 L 1352.1279296875 174.03391326857638 L 1353.078125 173.09067174575057 L 1354.0283203125 172.15582681149021 L 1354.978515625 171.2294385551096 L 1355.9287109375 170.31156718382465 L 1356.87890625 169.40227302282653 L 1357.8291015625 168.50161651521034 L 1358.779296875 167.6096582220415 L 1359.7294921875 166.72645882228676 L 1360.6796875 165.85207911286295 L 1361.6298828125 164.98658000863645 L 1362.580078125 164.13002254240587 L 1363.5302734375005 163.2824678648891 L 1364.48046875 162.4439772447488 L 1365.4306640625 161.61461206860236 L 1366.380859375 160.79443384097408 L 1367.3310546875 159.98350418435052 L 1368.28125 159.18188483914025 L 1369.2314453125 158.3896376636991 L 1370.181640625 157.60682463431226 L 1371.1318359375 156.83350784520223 L 1372.08203125 156.06974950852089 L 1373.0322265624995 155.3156119543777 L 1373.982421875 154.57115763079867 L 1374.9326171875 153.83644910375472 L 1375.8828125 153.11154905714886 L 1376.8330078125 152.39652029284116 L 1377.783203125 151.69142573058878 L 1378.7333984375 150.99632840813103 L 1379.68359375 150.31129148109437 L 1380.6337890625 149.6363782231099 L 1381.583984375 148.97165202566543 L 1382.5341796875005 148.317176398244 L 1383.484375 147.6730149682378 L 1384.4345703125 147.03923148099125 L 1385.3847656250005 146.41588979977098 L 1386.3349609375005 145.80305390579827 L 1387.2851562500005 145.20078789821116 L 1388.2353515625 144.6091559941002 L 1389.185546875 144.02822252848534 L 1390.1357421875 143.45805195431603 L 1391.0859375 142.89870884249933 L 1392.0361328125005 142.35025788185612 L 1392.986328125 141.8127638791501 L 1393.9365234375 141.2862917591143 L 1394.88671875 140.77090656434882 L 1395.8369140625 140.26667345545832 L 1396.787109375 139.7736577109522 L 1397.7373046875 139.29192472727698 L 1398.6875 138.82154001882122 L 1399.6376953125 138.3625692179055 L 1400.587890625 137.91507807481526 L 1401.5380859375005 137.4791324577103 L 1402.48828125 137.05479835276014 L 1403.4384765625 136.64214186401898 L 1404.388671875 136.24122921349795 L 1405.3388671875 135.8521267411428 L 1406.2890625 135.47490090482916 L 1407.2392578125 135.10961828038694 L 1408.189453125 134.75634556155592 L 1409.1396484375 134.41514956004528 L 1410.08984375 134.08609720547884 L 1411.0400390624995 133.76925554540514 L 1411.990234375 133.4646917453498 L 1412.9404296875 133.17247308874312 L 1413.890625 132.8926669769446 L 1414.8408203125 132.62534092928888 L 1415.791015625 132.37056258301493 L 1416.7412109375 132.1283996933089 L 1417.69140625 131.89892013328893 L 1418.6416015625 131.68219189402055 L 1419.591796875 131.47828308449857 L 1420.5419921874995 131.28726193164243 L 1421.4921875 131.10919678034418 L 1422.4423828125 130.9441560933999 L 1423.392578125 130.79220845154032 L 1424.3427734375 130.65342255345115 L 1425.2929687499995 130.5278672157549 L 1426.2431640624995 130.4156113730039 L 1427.193359375 130.31672407767985 L 1428.1435546875 130.23127450022173 L 1429.09375 130.15933192896796 L 1430.0439453124995 130.10096577023933 L 1430.994140625 130.05624554826352 L 1431.9443359375 130.02524090522297 L 1432.89453125 130.00802160120952 L 1433.8447265625 130.00465751428487 L 1434.7949218749995 130.01521864042263 L 1435.7451171874995 130.03977509354627 L 1436.6953125 130.07839710552093 L 1437.6455078125 130.13115502612686 L 1438.595703125 130.19811932309847 L 1439.5458984374995 130.27936058209764 L 1440.4960937499995 130.3749495067483 L 1441.4462890624995 130.484956918556 L 1442.3964843749995 130.6094537570242 L 1443.3466796875 130.74851107954794 L 1444.2968749999995 130.90220006149434 L 1445.2470703124995 131.07059199613798 L 1446.197265625 131.25375829472034 L 1447.1474609375 131.4517704863723 L 1448.09765625 131.66470021820714 L 1449.0478515624995 131.89261925526546 L 1449.998046875 132.1355994805068 L 1450.9482421875 132.39371289484848 L 1451.8984375 132.6670316171219 L 1452.8486328125 132.95562788411087 L 1453.798828125 133.25957405054135 L 1454.7490234375 133.57894258904878 L 1455.69921875 133.91380609024304 L 1456.6494140625 134.2642372626491 L 1457.599609375 134.63030893272105 L 1458.5498046874995 135.0120940448603 L 1459.5 135.40966566141287 L 1460.4501953125 135.82309696265452 L 1461.400390625 136.25246124678267 L 1462.3505859375 136.69783192994987 L 1463.3007812499995 137.15928254625317 L 1464.2509765624995 137.63688674768616 L 1465.201171875 138.13071830424553 L 1466.1513671875 138.64085110378915 L 1467.1015625 139.16735915216498 L 1468.0517578124995 139.71031657314825 L 1469.001953125 140.269797608408 L 1469.9521484375 140.84587661764158 L 1470.90234375 141.4386280783798 L 1471.8525390625 142.0481265861614 L 1472.802734375 142.67444685443172 L 1473.7529296875 143.31766371457832 L 1474.703125 143.977852115916 L 1475.6533203125 144.6550871257217 L 1476.603515625 145.3494439291818 L 1477.5537109375005 146.0609978294449 L 1478.50390625 146.78982424757407 L 1479.4541015625 147.53599872257723 L 1480.404296875 148.29959691139663 L 1481.3544921875 149.0806945889243 L 1482.3046875 149.879367647977 L 1483.2548828125 150.6956920993007 L 1484.205078125 151.52974407158877 L 1485.1552734375 152.3815998114818 L 1486.10546875 153.25133568352965 L 1487.0556640624995 154.1390281702395 L 1488.005859375 155.0447538720531 L 1488.9560546875 155.9685895073419 L 1489.90625 156.91061191243682 L 1490.8564453125 157.87089804155335 L 1491.806640625 158.84952496690426 L 1492.7568359375 159.84656987860944 L 1493.70703125 160.86211008469797 L 1494.6572265625 161.89622301120426 L 1495.607421875 162.94898620203912 L 1496.5576171874995 164.0204773190784 L 1497.5078125 165.11077414213503 L 1498.4580078125 166.21995456894638 L 1499.408203125 167.3480966151642 L 1500.3583984375 168.49527841444808 L 1501.3085937499995 169.66157821833417 L 1502.2587890624995 170.84707439630836 L 1503.208984375 172.05184543578844 L 1504.1591796875 173.27596994215207 L 1505.109375 174.51952663869417 L 1506.0595703124995 175.78259436664382 L 1507.009765625 177.06525208519258 L 1507.9599609375 178.36757887143892 L 1508.91015625 179.68965392041332 L 1509.8603515625 181.03155654512375 L 1510.8105468749995 182.39336617648758 L 1511.7607421874995 183.77516236334145 L 1512.7109375 185.17702477250987 L 1513.6611328125 186.59903318869112 L 1514.611328125 188.04126751455874 L 1515.5615234374995 189.5038077707179 L 1516.5117187499995 190.98673409573132 L 1517.4619140624995 192.49012674605103 L 1518.4121093749995 194.01406609609876 L 1519.3623046875 195.55863263821823 L 1520.3124999999995 197.12390698269792 L 1521.2626953124995 198.70996985777106 L 1522.212890625 200.31690210959505 L 1523.1630859375 201.94478470225715 L 1524.11328125 203.5936987178045 L 1525.0634765624995 205.26372535620328 L 1526.0136718749995 206.95494593534977 L 1526.9638671874995 208.66744189109443 L 1527.9140624999995 210.4012947772178 L 1528.8642578125 212.15658626545473 L 1529.8144531249995 213.93339814541957 L 1530.7646484374995 215.73181232474667 L 1531.7148437499995 217.55191082894464 L 1532.6650390624995 219.39377580146686 L 1533.6152343749995 221.25748950373122 L 1534.5654296874995 223.14313431506537 L 1535.5156249999995 225.05079273273634 L 1536.4658203124995 226.98054737198106 L 1537.4160156249995 228.93248096593084 L 1538.3662109375 230.9066763656616 L 1539.3164062499995 232.9032165402091 L 1540.2666015624995 234.92218457653348 L 1541.216796875 236.9636636794994 L 1542.1669921875 239.02773717197658 L 1543.1171875 241.11448849471878 L 1544.0673828124995 243.22400120641475 L 1545.017578125 245.35635898373778 L 1545.9677734375 247.51164562123563 L 1546.91796875 249.68994503145097 L 1547.8681640625 251.89134124480552 L 1548.8183593749995 254.11591840970118 L 1549.7685546874995 256.3637607924693 L 1550.71875 258.6349527773607 L 1551.6689453125 260.9295788665909 L 1552.619140625 263.2477236802699 L 1553.5693359374995 265.5894719564826 L 1554.5195312499995 267.9549085512482 L 1555.4697265624995 270.3441184385008 L 1556.4199218749995 272.75718671011873 L 1557.3701171875 275.1941985759254 L 1558.3203124999995 277.65523936367333 L 1559.2705078124995 280.1403945190549 L 1560.220703125 282.64974960570225 L 1561.1708984375 285.1833903051971 L 1562.12109375 287.74140241700024 L 1563.0712890624995 290.32387185859784 L 1564.021484375 292.93088466532504 L 1564.9716796875 295.562526990517 L 1565.921875 298.2188851054033 L 1566.8720703125 300.90004539919823 L 1567.822265625 303.60609437900064 L 1568.7724609375 306.3371186698889 L 1569.72265625 309.09320501484626 L 1570.6728515625 311.87444027481536 L 1571.623046875 314.68091142863307 L 1572.5732421874995 317.51270557314683 L 1573.5234375 320.3699099230879 L 1574.4736328125 323.2526118111173 L 1575.423828125 326.1608986878557 L 1576.3740234375 329.09485812189394 L 1577.3242187499995 332.0545777996713 L 1578.2744140624995 335.04014552564763 L 1579.224609375 338.05164922215704 L 1580.1748046875 341.0891769295333 L 1581.125 344.1528168059797 L 1582.0751953124995 347.2426571276993 L 1583.025390625 350.3587862887796 L 1583.9755859375 353.5012928012778 L 1584.92578125 356.6702652951708 L 1585.8759765625 359.86579251837986 L 1586.8261718749995 363.0879633367661 L 1587.7763671874995 366.33686673412006 L 1588.7265625 369.61259181218213 L 1589.6767578125 372.9152277905969 L 1590.626953125 376.24486400698396 L 1591.5771484374995 379.60158991687734 L 1592.5273437499995 382.98549509376073 L 1593.4775390624995 386.3966692290474 L 1594.4277343749995 389.8352021320802 L 1595.3779296875 393.30118373015665 L 1596.3281249999995 396.79470406849384 L 1597.2783203124995 400.3158533102283 L 1598.228515625 403.8647217365117 L 1599.1787109375 407.4413997463296 L 1600.12890625 411.0459778566778 L 1601.0791015624995 414.6785467024613 L 1602.029296875 418.33919703650474 L 1602.9794921875 422.0280197296077 L 1603.9296875 425.7451057704941 L 1604.8798828125 429.4905462658074 L 1605.830078125 433.2644324401258 L 1606.7802734375 437.0668556359921 L 1607.73046875 440.8979073138637 L 1608.6806640625 444.75767905216776 L 1609.630859375 448.64626254720065 L 1610.5810546874995 452.56374961326367 L 1611.53125 456.51023218256773 L 1612.4814453125 460.48580230524317 L 1613.431640625 464.49055214939006 L 1614.3818359375 468.5245740010281 L 1615.3320312499995 472.5879602641014 L 1616.2822265624995 476.68080346051903 L 1617.232421875 480.80319623010934 L 1618.1826171875 484.9552313306555 L 1619.1328125 489.1370016378251 L 1620.0830078124995 493.34860014529556 L 1621.033203125 497.59011996463374 L 1621.9833984375 501.86165432534114 L 1622.93359375 506.1632965748738 L 1623.8837890625 510.4951401786376 L 1624.833984375 514.8572787199479 L 1625.7841796875 519.2498059000645 L 1626.734375 523.672815538177 L 1627.6845703125 528.1264015714398 L 1628.634765625 532.6106580549215 L 1629.5849609375005 537.1256791616003 L 1630.53515625 541.6715591824795 L 1631.4853515625 546.2483925263765 L 1632.435546875 550.8562737201537 L 1633.3857421875 555.4952974085627 L 1634.3359375 560.165558354275 L 1635.2861328125 564.8671514379419 L 1636.236328125 569.6001716581136 L 1637.1865234375 574.3647141312905 L 1638.13671875 579.1608740919276 L 1639.0869140624995 583.9887468923844 L 1640.037109375 588.8484280029897 L 1640.9873046875 593.7400130119875 L 1641.9375 598.6635976255458 L 1642.8876953125 603.6192776678076 L 1643.837890625 608.6071490808306 L 1644.7880859375 613.6273079245967 L 1645.73828125 618.6798503770628 L 1646.6884765625 623.7648727340751 L 1647.638671875 628.8824714094394 L 1648.5888671874995 634.0327429349267 L 1649.5390625 639.2157839601816 L 1650.4892578125 644.4316912528444 L 1651.439453125 649.6805616984692 L 1652.3896484375 654.9624923005199 L 1653.3398437499995 660.2775801804503 L 1654.2900390624995 665.6259225776084 L 1655.240234375 671.0076168492972 L 1656.1904296875 676.4227604707539 L 1657.140625 681.8714510351508 L 1658.0908203124995 687.3537862536194 L 1659.041015625 692.8698639551759 L 1659.9912109375 698.4197820868011 L 1660.94140625 704.0036387134406 L 1661.8916015625 709.6215320179344 L 1662.841796875 715.2735603010872 L 1663.7919921875 720.9598219816182 L 1664.7421875 726.6804155962066 L 1665.6923828125 732.4354397994405 L 1666.642578125 738.2249933638631 L 1667.5927734375005 744.0491751799672 L 1668.54296875 749.9080842561451 L 1669.4931640625 755.8018197187688 L 1670.443359375 761.7304808120997 L 1671.3935546875 767.6941668984042 L 1672.34375 773.6929774577977 L 1673.2939453125 779.7270120884059 L 1674.244140625 785.7963705062436 L 1675.1943359375 791.9011525452954 L 1676.14453125 798.0414581574605 L 1677.0947265624995 804.2173874125826 L 1678.044921875 810.4290404984554 L 1678.9951171875 816.6765177207867 L 1679.9453125 822.959919503224 L 1680.8955078125 829.2793463873799 L 1681.845703125 835.6348990327558 L 1682.7958984375 842.0266782168335 L 1683.74609375 848.4547848350089 L 1684.6962890625 854.9193199006177 L 1685.646484375 861.4203845449553 L 1686.5966796875005 867.9580800171913 L 1687.546875 874.5325076845204 L 1688.4970703125 881.1437690319866 L 1689.447265625 887.7919656626387 L 1690.3974609375005 894.4771992974149 L 1691.3476562500005 901.1995717752283 L 1692.2978515625 907.9591850528961 L 1693.248046875 914.7561412052211 L 1694.1982421875 921.5905424248542 L 1695.1484375 928.4624910224774 L 1696.0986328125005 935.3720894266312 L 1697.048828125 942.3194401838665 L 1697.9990234375 949.3046459586335 L 1698.94921875 956.3278095333018 L 1699.8994140625 963.3890338082008 L 1700.849609375 970.4884218016148 L 1701.7998046875 977.626076649712 L 1702.75 984.8021016066358 L 1703.7001953125 992.0166000444641 L 1704.650390625 999.2696754532294 L 1705.6005859375005 1006.5614314408184 L 1706.55078125 1013.8919717331632 L 1707.5009765625 1021.2614001740749 L 1708.451171875 1028.6698207252841 L 1709.4013671875 1036.1173374665116 L 1710.3515625 1043.6040545953774 L 1711.3017578125 1051.1300764274313 L 1712.251953125 1058.6955073961924 L 1713.2021484375 1066.300452053115 L 1714.15234375 1073.9450150675418 L 1715.1025390624995 1081.629301226812 L 1716.052734375 1089.3534154361523 L 1717.0029296875 1097.117462718771 L 1717.953125 1104.9215482157795 L 1718.9033203125 1112.7657771862293 L 1719.853515625 1120.6502550071218 L 1720.8037109375 1128.575087173408 L 1721.75390625 1136.5403792979378 L 1722.7041015625 1144.5462371115063 L 1723.654296875 1152.5927664628884 L 1724.6044921875005 1160.680073318758 L 1725.5546875 1168.8082637636992 L 1726.5048828125 1176.9774440003102 L 1727.455078125 1185.1877203490342 L 1728.4052734375005 1193.4391992483438 L 1729.3554687500005 1201.731987254581 L 1730.3056640625 1210.066191042023 L 1731.255859375 1218.4419174029363 L 1732.2060546875 1226.8592732474967 L 1733.15625 1235.318365603815 L 1734.1064453125005 1243.8193016179116 L 1735.056640625 1252.3621885537764 L 1736.0068359375 1260.9471337933587 L 1736.95703125 1269.5742448364776 L 1737.9072265625 1278.2436293009673 L 1738.857421875 1286.9553949225258 L 1739.8076171875 1295.709649554831 L 1740.7578125 1304.5065011694703 L 1741.7080078125 1313.3460578560064 L 1742.658203125 1322.2284278219256 L 1743.6083984375005 1331.1537193926297 L 1744.55859375 1340.1220410114643 L 1745.5087890625 1349.1335012397049 L 1746.458984375 1358.188208756597 L 1747.4091796875005 1367.2862723593007 L 1748.3593750000005 1376.4278009628997 L 1749.3095703125 1385.6129036004234 L 1750.2597656250005 1394.8416894228653 L 1751.2099609375005 1404.1142676991342 L 1752.1601562500005 1413.4307478160572 L 1753.1103515625005 1422.7912392784174 L 1754.060546875 1432.195851708926 L 1755.0107421875 1441.6446948482458 L 1755.9609375 1451.1378785549923 L 1756.9111328125005 1460.6755128056666 L 1757.8613281250005 1470.2577076947343 L 1758.8115234375 1479.8845734345905 L 1759.76171875 1489.5562203555796 L 1763.5625 1528.6928305854785 L 1824.375 2258.4389360692626 L 1885.1875 3204.1222192361547 L 1946 4397.803130935288" display="inline"></path></g><g></g><g></g><g></g><g>
			<text id="jxgboxPoly_jxgBoard1L3_ticks_15Label1" style="position: absolute; white-space: nowrap; font-family: Arial, Helvetica, Geneva, sans-serif; font-size: 12px; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: inherit;" fill="black" fill-opacity="1" class="JXGtext" x="278px" text-anchor="middle" y="874.5484199796126px" dy="1.6ex" display="inline" _mstTextHash="4459" _mstHash="632">1</text>
			<text id="jxgboxPoly_jxgBoard1L3_ticks_110Label2" style="position: absolute; white-space: nowrap; font-family: Arial, Helvetica, Geneva, sans-serif; font-size: 12px; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: inherit;" fill="black" fill-opacity="1" class="JXGtext" x="432.44444444444434px" text-anchor="middle" y="874.5484199796126px" dy="1.6ex" display="inline" _mstTextHash="4550" _mstHash="631">2</text>
			<text id="jxgboxPoly_jxgBoard1L3_ticks_115Label3" style="position: absolute; white-space: nowrap; font-family: Arial, Helvetica, Geneva, sans-serif; font-size: 12px; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: inherit;" fill="black" fill-opacity="1" class="JXGtext" x="586.8888888888889px" text-anchor="middle" y="874.5484199796126px" dy="1.6ex" display="inline" _mstTextHash="4641" _mstHash="630">3</text>
			<text id="jxgboxPoly_jxgBoard1L3_ticks_120Label4" style="position: absolute; white-space: nowrap; font-family: Arial, Helvetica, Geneva, sans-serif; font-size: 12px; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: inherit;" fill="black" fill-opacity="1" class="JXGtext" x="741.3333333333334px" text-anchor="middle" y="874.5484199796126px" dy="1.6ex" display="inline" _mstTextHash="4732" _mstHash="629">4</text>
			<text id="jxgboxPoly_jxgBoard1L3_ticks_125Label5" style="position: absolute; white-space: nowrap; font-family: Arial, Helvetica, Geneva, sans-serif; font-size: 12px; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: inherit;" fill="black" fill-opacity="1" class="JXGtext" x="895.7777777777779px" text-anchor="middle" y="874.5484199796126px" dy="1.6ex" display="inline" _mstTextHash="4823" _mstHash="628">5</text>
			<text id="jxgboxPoly_jxgBoard1L3_ticks_130Label6" style="position: absolute; white-space: nowrap; font-family: Arial, Helvetica, Geneva, sans-serif; font-size: 12px; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: inherit;" fill="black" fill-opacity="1" class="JXGtext" x="1050.2222222222226px" text-anchor="middle" y="874.5484199796126px" dy="1.6ex" display="inline" _mstTextHash="4914" _mstHash="627">6</text>
			<text id="jxgboxPoly_jxgBoard1L3_ticks_135Label7" style="position: absolute; white-space: nowrap; font-family: Arial, Helvetica, Geneva, sans-serif; font-size: 12px; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: inherit;" fill="black" fill-opacity="1" class="JXGtext" x="1204.666666666667px" text-anchor="middle" y="874.5484199796126px" dy="1.6ex" display="inline" _mstTextHash="5005" _mstHash="626">7</text>
			<text id="jxgboxPoly_jxgBoard1L3_ticks_140Label8" style="position: absolute; white-space: nowrap; font-family: Arial, Helvetica, Geneva, sans-serif; font-size: 12px; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: inherit;" fill="black" fill-opacity="1" class="JXGtext" x="1359.1111111111113px" text-anchor="middle" y="874.5484199796126px" dy="1.6ex" display="inline" _mstTextHash="5096" _mstHash="625">8</text>
			<text id="jxgboxPoly_jxgBoard1L3_ticks_145Label9" style="position: absolute; white-space: nowrap; font-family: Arial, Helvetica, Geneva, sans-serif; font-size: 12px; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: inherit;" fill="black" fill-opacity="1" class="JXGtext" x="1513.5555555555552px" text-anchor="middle" y="874.5484199796126px" dy="1.6ex" display="inline" _mstTextHash="5187" _mstHash="624">9</text>
			<text id="jxgboxPoly_jxgBoard1L3_ticks_150Label10" style="position: absolute; white-space: nowrap; font-family: Arial, Helvetica, Geneva, sans-serif; font-size: 12px; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: inherit;" fill="black" fill-opacity="1" class="JXGtext" x="1667.999999999999px" text-anchor="middle" y="874.5484199796126px" dy="1.6ex" display="inline" _mstTextHash="9451" _mstHash="623">10</text>
			<text id="jxgboxPoly_jxgBoard1L3_ticks_155Label11" style="position: absolute; white-space: nowrap; font-family: Arial, Helvetica, Geneva, sans-serif; font-size: 12px; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: inherit;" fill="black" fill-opacity="1" class="JXGtext" x="1822.444444444443px" text-anchor="middle" y="874.5484199796126px" dy="1.6ex" display="inline" _mstTextHash="9555" _mstHash="622">11</text>
			<text id="jxgboxPoly_jxgBoard1L18_ticks_15Label1" style="position: absolute; white-space: nowrap; font-family: Arial, Helvetica, Geneva, sans-serif; font-size: 12px; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: inherit;" fill="black" fill-opacity="1" class="JXGtext" x="117.55555555555554px" text-anchor="end" y="694.4332313965341px" dy="0.6ex" display="inline" _mstTextHash="15353" _mstHash="621">0.5</text>
			<text id="jxgboxPoly_jxgBoard1L18_ticks_110Label2" style="position: absolute; white-space: nowrap; font-family: Arial, Helvetica, Geneva, sans-serif; font-size: 12px; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: inherit;" fill="black" fill-opacity="1" class="JXGtext" x="117.55555555555554px" text-anchor="end" y="517.3180428134557px" dy="0.6ex" display="inline" _mstTextHash="4459" _mstHash="620">1</text>
			<text id="jxgboxPoly_jxgBoard1L18_ticks_115Label3" style="position: absolute; white-space: nowrap; font-family: Arial, Helvetica, Geneva, sans-serif; font-size: 12px; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: inherit;" fill="black" fill-opacity="1" class="JXGtext" x="117.55555555555554px" text-anchor="end" y="340.20285423037706px" dy="0.6ex" display="inline" _mstTextHash="15444" _mstHash="619">1.5</text>
			<text id="jxgboxPoly_jxgBoard1L18_ticks_120Label4" style="position: absolute; white-space: nowrap; font-family: Arial, Helvetica, Geneva, sans-serif; font-size: 12px; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: inherit;" fill="black" fill-opacity="1" class="JXGtext" x="117.55555555555554px" text-anchor="end" y="163.08766564729854px" dy="0.6ex" display="inline" _mstTextHash="4550" _mstHash="618">2</text>
			<ellipse id="jxgboxPoly_jxgBoard1P24" style="position: absolute; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: inherit;" stroke="red" stroke-opacity="1" stroke-width="2px" fill="red" fill-opacity="1" cx="278" cy="214" rx="3" ry="3" display="inline"></ellipse><ellipse id="jxgboxPoly_jxgBoard1P26" style="position: absolute; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: inherit;" stroke="red" stroke-opacity="1" stroke-width="2px" fill="red" fill-opacity="1" cx="432" cy="173" rx="3" ry="3" display="inline"></ellipse><ellipse id="jxgboxPoly_jxgBoard1P28" style="position: absolute; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: inherit;" stroke="red" stroke-opacity="1" stroke-width="2px" fill="red" fill-opacity="1" cx="587" cy="456" rx="3" ry="3" display="inline"></ellipse><ellipse id="jxgboxPoly_jxgBoard1P30" style="position: absolute; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: inherit;" stroke="red" stroke-opacity="1" stroke-width="2px" fill="red" fill-opacity="1" cx="741" cy="773" rx="3" ry="3" display="inline"></ellipse><ellipse id="jxgboxPoly_jxgBoard1P32" style="position: absolute; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: inherit;" stroke="red" stroke-opacity="1" stroke-width="2px" fill="red" fill-opacity="1" cx="896" cy="834" rx="3" ry="3" display="inline"></ellipse><ellipse id="jxgboxPoly_jxgBoard1P34" style="position: absolute; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: inherit;" stroke="red" stroke-opacity="1" stroke-width="2px" fill="red" fill-opacity="1" cx="1050" cy="601" rx="3" ry="3" display="inline"></ellipse><ellipse id="jxgboxPoly_jxgBoard1P36" style="position: absolute; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: inherit;" stroke="red" stroke-opacity="1" stroke-width="2px" fill="red" fill-opacity="1" cx="1205" cy="251" rx="3" ry="3" display="inline"></ellipse><ellipse id="jxgboxPoly_jxgBoard1P38" style="position: absolute; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: inherit;" stroke="red" stroke-opacity="1" stroke-width="2px" fill="red" fill-opacity="1" cx="1359" cy="139" rx="3" ry="3" display="inline"></ellipse><ellipse id="jxgboxPoly_jxgBoard1P40" style="position: absolute; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: inherit;" stroke="red" stroke-opacity="1" stroke-width="2px" fill="red" fill-opacity="1" cx="1514" cy="345" rx="3" ry="3" display="inline"></ellipse><ellipse id="jxgboxPoly_jxgBoard1P42" style="position: absolute; transition: fill 100ms ease 0s, fill-opacity 100ms ease 0s, stroke 100ms ease 0s, stroke-opacity 100ms ease 0s; visibility: inherit;" stroke="red" stroke-opacity="1" stroke-width="2px" fill="red" fill-opacity="1" cx="1668" cy="683" rx="3" ry="3" display="inline"></ellipse></g><g></g><g></g><g></g><g></g><g></g><g></g><g></g><g></g><g></g><g></g><foreignobject x="0" y="0" width="100%" height="100%" id="jxgboxPoly_foreignObj"></foreignobject></svg>
			<div class="JXGinfobox" id="jxgboxPoly_jxgBoard1_infobox" style="position: absolute; z-index: 9; font-family: Arial, Helvetica, Geneva, sans-serif; font-size: 12px; color: rgb(187, 187, 187); opacity: 1; inset: 871px auto auto 124px; visibility: hidden;" display="none" _msttexthash="14560" _msthash="633">0,0</div>
			<div id="jxgboxPoly_navigationbar" style="color: rgb(51, 51, 51); background-color: transparent; padding: 2px; position: absolute; font-size: 14px; cursor: pointer; z-index: 100; right: 5px; bottom: 5px;" class="JXG_navigation" _msttexthash="5902715" _msthash="617">
			<span style="padding-left: 7px; padding-right: 7px;" class="JXG_navigation_button">–</span>
			<span style="padding-left: 7px; padding-right: 7px;" class="JXG_navigation_button">o</span>
			<span style="padding-left: 7px; padding-right: 7px;" class="JXG_navigation_button">+</span>
			<span style="padding-left: 7px; padding-right: 7px;" class="JXG_navigation_button">←</span>
			<span style="padding-left: 7px; padding-right: 7px;" class="JXG_navigation_button">↓</span>
			<span style="padding-left: 7px; padding-right: 7px;" class="JXG_navigation_button">↑</span>
			<span style="padding-left: 7px; padding-right: 7px;" class="JXG_navigation_button">→</span>
			</div>
			<div class="JXGtext" id="jxgboxPoly_jxgBoard1P24Label" style="position: absolute; z-index: 9; font-family: Arial, Helvetica, Geneva, sans-serif; font-size: 12px; transition: color 100ms ease 0s, opacity 100ms ease 0s; color: black; opacity: 1; inset: 197px auto auto 288px; visibility: inherit;" display="inline" _msttexthash="265317" _msthash="616">P1 powiedział:</div>
			<div class="JXGtext" id="jxgboxPoly_jxgBoard1P26Label" style="position: absolute; z-index: 9; font-family: Arial, Helvetica, Geneva, sans-serif; font-size: 12px; transition: color 100ms ease 0s, opacity 100ms ease 0s; color: black; opacity: 1; inset: 156px auto auto 442px; visibility: inherit;" display="inline" _msttexthash="265421" _msthash="615">P2 powiedział:</div>
			<div class="JXGtext" id="jxgboxPoly_jxgBoard1P28Label" style="position: absolute; z-index: 9; font-family: Arial, Helvetica, Geneva, sans-serif; font-size: 12px; transition: color 100ms ease 0s, opacity 100ms ease 0s; color: black; opacity: 1; inset: 439px auto auto 597px; visibility: inherit;" display="inline" _msttexthash="265525" _msthash="614">P3 powiedział:</div>
			<div class="JXGtext" id="jxgboxPoly_jxgBoard1P30Label" style="position: absolute; z-index: 9; font-family: Arial, Helvetica, Geneva, sans-serif; font-size: 12px; transition: color 100ms ease 0s, opacity 100ms ease 0s; color: black; opacity: 1; inset: 756px auto auto 751px; visibility: inherit;" display="inline" _msttexthash="265629" _msthash="613">P4 powiedział:</div>
			<div class="JXGtext" id="jxgboxPoly_jxgBoard1P32Label" style="position: absolute; z-index: 9; font-family: Arial, Helvetica, Geneva, sans-serif; font-size: 12px; transition: color 100ms ease 0s, opacity 100ms ease 0s; color: black; opacity: 1; inset: 817px auto auto 906px; visibility: inherit;" display="inline" _msttexthash="265733" _msthash="612">P5 powiedział:</div>
			<div class="JXGtext" id="jxgboxPoly_jxgBoard1P34Label" style="position: absolute; z-index: 9; font-family: Arial, Helvetica, Geneva, sans-serif; font-size: 12px; transition: color 100ms ease 0s, opacity 100ms ease 0s; color: black; opacity: 1; inset: 584px auto auto 1060px; visibility: inherit;" display="inline" _msttexthash="265837" _msthash="611">P6 powiedział:</div>
			<div class="JXGtext" id="jxgboxPoly_jxgBoard1P36Label" style="position: absolute; z-index: 9; font-family: Arial, Helvetica, Geneva, sans-serif; font-size: 12px; transition: color 100ms ease 0s, opacity 100ms ease 0s; color: black; opacity: 1; inset: 234px auto auto 1215px; visibility: inherit;" display="inline" _msttexthash="265941" _msthash="610">P7 powiedział:</div>
			<div class="JXGtext" id="jxgboxPoly_jxgBoard1P38Label" style="position: absolute; z-index: 9; font-family: Arial, Helvetica, Geneva, sans-serif; font-size: 12px; transition: color 100ms ease 0s, opacity 100ms ease 0s; color: black; opacity: 1; inset: 122px auto auto 1369px; visibility: inherit;" display="inline" _msttexthash="266045" _msthash="609">P8 powiedział:</div>
			<div class="JXGtext" id="jxgboxPoly_jxgBoard1P40Label" style="position: absolute; z-index: 9; font-family: Arial, Helvetica, Geneva, sans-serif; font-size: 12px; transition: color 100ms ease 0s, opacity 100ms ease 0s; color: black; opacity: 1; inset: 328px auto auto 1523px; visibility: inherit;" display="inline" _msttexthash="266149" _msthash="608">P9 powiedział:</div>
			<div class="JXGtext" id="jxgboxPoly_jxgBoard1P42Label" style="position: absolute; z-index: 9; font-family: Arial, Helvetica, Geneva, sans-serif; font-size: 12px; transition: color 100ms ease 0s, opacity 100ms ease 0s; color: black; opacity: 1; inset: 666px auto auto 1678px; visibility: inherit;" display="inline" _msttexthash="288509" _msthash="607">P10 powiedział:</div>
			</div>
 			<form name="R4" onsubmit="javascript:void(0)">
				<div class="table">
					<div class="table-row">
						<div class="table-cell" title="Ranges of the axis for the calculation and display.">
							<p _msttexthash="162916" _msthash="28">Zakresy osi</p>
						</div>
						<div class="table-cell" title="Minimal value for x-axis.">
						<font _mstmutation="1" _msttexthash="67249" _msthash="29">
							x-min=  </font>
							<input onfocus="this.select()" type="number" name="min" value="-10" onchange="Resize()" class="Eingabe">
						</div>
						<div class="table-cell" title="Maximal value for x-axis.">
						<font _mstmutation="1" _msttexthash="67639" _msthash="30">
							x-max=  </font>
							<input onfocus="this.select()" type="number" name="max" value="10" onchange="Resize()" class="Eingabe">
						</div>
						<div class="table-cell" title="Minimal value for y-axis.">
						<font _mstmutation="1" _msttexthash="67340" _msthash="31">
							y-min=  </font>
							<input onfocus="this.select()" type="number" name="ymin" value="-5" onchange="Resize()" class="Eingabe">
						</div>
						<div class="table-cell" title="Maximal value for y-axis.">
						<font _mstmutation="1" _msttexthash="67730" _msthash="32">
							y-max=  </font>
							<input onfocus="this.select()" type="number" name="ymax" value="5" onchange="Resize()" class="Eingabe">
						</div>
					</div>
				</div>
			</form>
			<div class="table">
				<div class="table-row">
				</div>
			</div>
			<div class="table">
				<div class="table-row">
					<div class="table-cell" title="Setting the line size and line color of the regression line.">
					<font _mstmutation="1" _msttexthash="146484" _msthash="146"> Wielomian:</font>
					<input id="Poly" type="number" class="EingabeS" name="m" value="4" onchange="digitfkt()">
					</div>
					<div class="table-cell">
						<span class="MathJax_Preview" style="color: inherit; display: none;" _msthidden="8"></span>
						<span class="MathJax" id="MathJax-Element-5-Frame" tabindex="0" style="position: relative;" data-mathml="&lt;math xmlns=&quot;http://www.w3.org/1998/Math/MathML&quot;&gt;&lt;mi _msttexthash=&quot;9282&quot; _msthash=&quot;147&quot;&gt;f&lt;/mi&gt;&lt;mrow&gt;&lt;mo&gt;(&lt;/mo&gt;&lt;mi _msttexthash=&quot;10920&quot; _msthash=&quot;148&quot;&gt;x&lt;/mi&gt;&lt;mo&gt;)&lt;/mo&gt;&lt;/mrow&gt;&lt;mo&gt;=&lt;/mo&gt;&lt;msub&gt;&lt;mi _msttexthash=&quot;8827&quot; _msthash=&quot;149&quot;&gt;a&lt;/mi&gt;&lt;mn _msttexthash=&quot;4368&quot; _msthash=&quot;150&quot;&gt;0&lt;/mn&gt;&lt;/msub&gt;&lt;mo&gt;+&lt;/mo&gt;&lt;msub&gt;&lt;mi _msttexthash=&quot;8827&quot; _msthash=&quot;151&quot;&gt;a&lt;/mi&gt;&lt;mn _msttexthash=&quot;4459&quot; _msthash=&quot;152&quot;&gt;1&lt;/mn&gt;&lt;/msub&gt;&lt;mo _msttexthash=&quot;809991&quot; _msthash=&quot;153&quot;&gt;&amp;#x22C5;&lt;/mo&gt;&lt;mi _msttexthash=&quot;10920&quot; _msthash=&quot;154&quot;&gt;x&lt;/mi&gt;&lt;mo&gt;+&lt;/mo&gt;&lt;msub&gt;&lt;mi _msttexthash=&quot;8827&quot; _msthash=&quot;155&quot;&gt;a&lt;/mi&gt;&lt;mn _msttexthash=&quot;4550&quot; _msthash=&quot;156&quot;&gt;2&lt;/mn&gt;&lt;/msub&gt;&lt;mo _msttexthash=&quot;809991&quot; _msthash=&quot;157&quot;&gt;&amp;#x22C5;&lt;/mo&gt;&lt;msup&gt;&lt;mi _msttexthash=&quot;10920&quot; _msthash=&quot;158&quot;&gt;x&lt;/mi&gt;&lt;mn _msttexthash=&quot;4550&quot; _msthash=&quot;159&quot;&gt;2&lt;/mn&gt;&lt;/msup&gt;&lt;mo&gt;+&lt;/mo&gt;&lt;mi _msttexthash=&quot;14352&quot; _msthash=&quot;160&quot;&gt;...&lt;/mi&gt;&lt;/math&gt;" role="presentation">
						<div class="table-row" style="height:150px;">
						<div class="table-cell" id="s9" title="Calculated fourier series">
						<p class="MJX_Assistive_MathML" role="presentation"><math><mi _msttexthash="9282" _msthash="147" _mstTextHash="9282" _mstHash="479">f</mi><mrow><mo>(</mo><mi _msttexthash="10920" _msthash="148" _mstTextHash="10920" _mstHash="480">x</mi><mo>)</mo></mrow><mo>=</mo><msub><mi _msttexthash="8827" _msthash="149" _mstTextHash="8827" _mstHash="481">a</mi><mn _msttexthash="4368" _msthash="150" _mstTextHash="4368" _mstHash="482">0</mn></msub><mo>+</mo><msub><mi _msttexthash="8827" _msthash="151" _mstTextHash="8827" _mstHash="483">a</mi><mn _msttexthash="4459" _msthash="152" _mstTextHash="4459" _mstHash="484">1</mn></msub><mo _msttexthash="809991" _msthash="153" _mstTextHash="809991" _mstHash="485">⋅</mo><mi _msttexthash="10920" _msthash="154" _mstTextHash="10920" _mstHash="486">x</mi><mo>+</mo><msub><mi _msttexthash="8827" _msthash="155" _mstTextHash="8827" _mstHash="487">a</mi><mn _msttexthash="4550" _msthash="156" _mstTextHash="4550" _mstHash="488">2</mn></msub><mo _msttexthash="809991" _msthash="157" _mstTextHash="809991" _mstHash="489">⋅</mo><msup><mi _msttexthash="10920" _msthash="158" _mstTextHash="10920" _mstHash="490">x</mi><mn _msttexthash="4550" _msthash="159" _mstTextHash="4550" _mstHash="491">2</mn></msup><mo>+</mo><mi _msttexthash="14352" _msthash="160" _mstTextHash="14352" _mstHash="492">...</mi></math>
						</p>
						</div>
						</div>
						</div>
						</span>
						
						<script type="math/mml" id="MathJax-Element-5"><math><mi _msttexthash="9282" _msthash="147">f</mi><mrow><mo>(</mo><mi _msttexthash="10920" _msthash="148">x</mi><mo>)</mo></mrow><mo>=</mo><msub><mi _msttexthash="8827" _msthash="149">a</mi><mn _msttexthash="4368" _msthash="150">0</mn></msub><mo>+</mo><msub><mi _msttexthash="8827" _msthash="151">a</mi><mn _msttexthash="4459" _msthash="152">1</mn></msub><mo _msttexthash="809991" _msthash="153">⋅</mo><mi _msttexthash="10920" _msthash="154">x</mi><mo>+</mo><msub><mi _msttexthash="8827" _msthash="155">a</mi><mn _msttexthash="4550" _msthash="156">2</mn></msub><mo _msttexthash="809991" _msthash="157">⋅</mo><msup><mi _msttexthash="10920" _msthash="158">x</mi><mn _msttexthash="4550" _msthash="159">2</mn></msup><mo>+</mo><mi _msttexthash="14352" _msthash="160">...</mi></math>
						</script>
					</div>
				</div>
				<div class="table-row">
				</div>
				<div class="table-row">
					<div class="table-cell">
						<input type="checkbox" id="PolyV" name="fitting" onchange="Resize();" checked="">
					</div>
					<div class="table-cell">
						<select id="SelectLine3" class="select" onchange="Resize();">
						  <option value="0" _msttexthash="47554" _msthash="161">żaden</option>
						  <option value="1" selected="" _msttexthash="140868" _msthash="162">bardzo mały</option>
						  <option value="2" _msttexthash="62634" _msthash="163">mały</option>
						  <option value="3" _msttexthash="79781" _msthash="164">normalny</option>
						  <option value="4" _msttexthash="61828" _msthash="165">gruby</option>
						  <option value="5" _msttexthash="139750" _msthash="166">bardzo gruby</option>
						  <option value="6" _msttexthash="36036" _msthash="167">XXL</option>
						  <option value="7" _msttexthash="51480" _msthash="168">xxxl (xxxl)</option>
						  <option value="8" _msttexthash="68484" _msthash="169">xxxxl</option>
						</select>
						<select id="SelectColor3" class="select" onchange="Resize();">
						  <option value="red" _msttexthash="32578" _msthash="170">czerwony</option>
						  <option value="black" _msttexthash="59670" _msthash="171">czarny</option>
						  <option value="blue" selected="" _msttexthash="46969" _msthash="172">niebieski</option>
						  <option value="green" _msttexthash="61906" _msthash="173">zielony</option>
						  <option value="magenta" _msttexthash="95407" _msthash="174">magenta</option>
						  <option value="cyan" _msttexthash="143169" _msthash="175">turkus</option>
						  <option value="yellow" _msttexthash="82628" _msthash="176">żółty</option>
						  <option value="gray" _msttexthash="48308" _msthash="177">szary</option>
						</select>
						<select id="dash3" class="select" onchange="Resize();">
						  <option value="0" selected="" _msttexthash="136903" _msthash="178">linia ciągła</option>
						  <option value="1" _msttexthash="14352" _msthash="179">...</option>
						  <option value="2">-</option>
						  <option value="3">--</option>
						  <option value="4">---</option>
						  <option value="5">--  ---</option>
						  <option value="6">-- ---</option>
						</select>
					</div>
				</div>
				<div class="table-row">
					<div class="table-cell" title="Setting the line size and line color of the regression line.">
					<font _mstmutation="1" _msttexthash="271999" _msthash="208"> Szereg Fouriera:</font>
					<input id="Fourier" type="number" class="EingabeS" name="k" value="4" onchange="digitfkt()">
					</div>
					<div class="table-cell">
						<span class="MathJax_Preview" style="color: inherit; display: none;" _msthidden="6"></span>
						<div class="table">
						<div class="table-cell" id="s9" title="Calculated fourier series">
						<p class="FormelBoxL"><math><mi>f</mi><mrow><mo>(</mo><mi>x</mi><mo>)</mo></mrow><mo>=</mo><mfrac><msub><mi>a</mi><mn>0</mn></msub><mn>2</mn></mfrac><mo>+</mo><munderover><mo>∑</mo><mrow><mi>k</mi><mo>=</mo><mn>1</mn></mrow><mi>n</mi></munderover><mrow><mo>(</mo><msub><mi>a</mi><mi>k</mi></msub><mo>cos</mo><mrow><mo>(</mo><mi>k</mi><mi>ω</mi><mi>x</mi><mo>)</mo></mrow><mo>+</mo><msub><mi>b</mi><mi>k</mi></msub><mo>sin</mo><mrow><mo>(</mo><mi>k</mi><mi>ω</mi><mi>x</mi><mo>)</mo></mrow><mo>)</mo></mrow><mo>=</mo><mfrac><mn>1.301</mn><mn>2</mn></mfrac><mo>+</mo><mn>0.560</mn><mo>⋅</mo><mo>cos</mo><mrow><mo>(</mo><mn>0.698</mn><mi>⋅</mi><mi>x</mi><mo>)</mo></mrow><mo>+</mo><mn>0.000</mn><mo>⋅</mo><mo>sin</mo><mrow><mo>(</mo><mn>0.698</mn><mi>⋅</mi><mi>x</mi><mo>)</mo></mrow><mo>-</mo><mn>0.247</mn><mo>⋅</mo><mo>cos</mo><mrow><mo>(</mo><mn>1.396</mn><mi>⋅</mi><mi>x</mi><mo>)</mo></mrow><mo>+</mo><mn>0.000</mn><mo>⋅</mo><mo>sin</mo><mrow><mo>(</mo><mn>1.396</mn><mi>⋅</mi><mi>x</mi><mo>)</mo></mrow><mo>-</mo><mn>0.028</mn><mo>⋅</mo><mo>cos</mo><mrow><mo>(</mo><mn>2.094</mn><mi>⋅</mi><mi>x</mi><mo>)</mo></mrow><mo>+</mo><mn>0.000</mn><mo>⋅</mo><mo>sin</mo><mrow><mo>(</mo><mn>2.094</mn><mi>⋅</mi><mi>x</mi><mo>)</mo></mrow><mo>+</mo><mn>0.125</mn><mo>⋅</mo><mo>cos</mo><mrow><mo>(</mo><mn>2.793</mn><mi>⋅</mi><mi>x</mi><mo>)</mo></mrow><mo>+</mo><mn>0.000</mn><mo>⋅</mo><mo>sin</mo><mrow><mo>(</mo><mn>2.793</mn><mi>⋅</mi><mi>x</mi><mo>)</mo></mrow></math></p></div>
						</div>
			</div>
						<script type="math/mml" id="MathJax-Element-7"><math><mi _msttexthash="9282" _msthash="209">f</mi><mrow><mo>(</mo><mi _msttexthash="10920" _msthash="210">x</mi><mo>)</mo></mrow><mo>=</mo><mfrac><msub><mi _msttexthash="8827" _msthash="211">a</mi><mn _msttexthash="4368" _msthash="212">0</mn></msub><mn _msttexthash="4550" _msthash="213">2</mn></mfrac><mo>+</mo><munderover><mo _msttexthash="793611" _msthash="214">∑</mo><mrow><mi _msttexthash="9737" _msthash="215">k</mi><mo>=</mo><mn _msttexthash="4459" _msthash="216">1</mn></mrow><mi _msttexthash="10010" _msthash="217">n</mi></munderover><mrow><mo>(</mo><msub><mi _msttexthash="8827" _msthash="218">a</mi><mi _msttexthash="9737" _msthash="219">k</mi></msub><mo _msttexthash="34008" _msthash="220">cos</mo><mrow><mo>(</mo><mi _msttexthash="9737" _msthash="221">k</mi><mi _msttexthash="88179" _msthash="222">ω</mi><mi _msttexthash="10920" _msthash="223">x</mi><mo>)</mo></mrow><mo>+</mo><msub><mi _msttexthash="8918" _msthash="224">b</mi><mi _msttexthash="9737" _msthash="225">k</mi></msub><mo _msttexthash="34255" _msthash="226">sin</mo><mrow><mo>(</mo><mi _msttexthash="9737" _msthash="227">k</mi><mi _msttexthash="88179" _msthash="228">ω</mi><mi _msttexthash="10920" _msthash="229">x</mi><mo>)</mo></mrow><mo>)</mo></mrow></math></script>
					</div>
				</div>
				<div class="table-row">
				</div>
				<div class="table-row">
					<div class="table-cell">
						<input type="checkbox" id="FourierV" name="fitting" onchange="Resize();">
					</div>
					<div class="table-cell">
						<select id="SelectLine6" class="select" onchange="Resize();">
						  <option value="0" _msttexthash="47554" _msthash="230">żaden</option>
						  <option value="1" _msttexthash="140868" _msthash="231">bardzo mały</option>
						  <option value="2" selected="" _msttexthash="62634" _msthash="232">mały</option>
						  <option value="3" _msttexthash="79781" _msthash="233">normalny</option>
						  <option value="4" _msttexthash="61828" _msthash="234">gruby</option>
						  <option value="5" _msttexthash="139750" _msthash="235">bardzo gruby</option>
						  <option value="6" _msttexthash="36036" _msthash="236">XXL</option>
						  <option value="7" _msttexthash="51480" _msthash="237">xxxl (xxxl)</option>
						  <option value="8" _msttexthash="68484" _msthash="238">xxxxl</option>
						</select>
						<select id="SelectColor6" class="select" onchange="Resize();">
						  <option value="red" _msttexthash="32578" _msthash="239">czerwony</option>
						  <option value="black" _msttexthash="59670" _msthash="240">czarny</option>
						  <option value="blue" _msttexthash="46969" _msthash="241">niebieski</option>
						  <option value="green" _msttexthash="61906" _msthash="242">zielony</option>
						  <option value="magenta" selected="" _msttexthash="95407" _msthash="243">magenta</option>
						  <option value="cyan" _msttexthash="143169" _msthash="244">turkus</option>
						  <option value="yellow" _msttexthash="82628" _msthash="245">żółty</option>
						  <option value="gray" _msttexthash="48308" _msthash="246">szary</option>
						</select>
						<select id="dash6" class="select" onchange="Resize();">
						  <option value="0" _msttexthash="136903" _msthash="247">linia ciągła</option>
						  <option value="1" _msttexthash="14352" _msthash="248">...</option>
						  <option value="2" selected="">-</option>
						  <option value="3">--</option>
						  <option value="4">---</option>
						  <option value="5">--  ---</option>
						  <option value="6">-- ---</option>
						</select>
					</div>
				</div>
				<div class="table-row">
					<div class="table-cell" title="Setting the line size and line color of the regression line." _msttexthash="131391" _msthash="279"> Punktów: </div>
					<div class="table-cell">
						<input type="checkbox" id="PointsV" name="fitting" onchange="Resize();" checked="">
						<select id="SelectPsize" class="select" onchange="Resize();">
						  <option value="0" _msttexthash="47554" _msthash="280">żaden</option>
						  <option value="1" _msttexthash="140868" _msthash="281">bardzo mały</option>
						  <option value="2" selected="" _msttexthash="62634" _msthash="282">mały</option>
						  <option value="3" _msttexthash="79781" _msthash="283">normalny</option>
						  <option value="4" _msttexthash="61828" _msthash="284">gruby</option>
						  <option value="5" _msttexthash="139750" _msthash="285">bardzo gruby</option>
						  <option value="6" _msttexthash="36036" _msthash="286">XXL</option>
						  <option value="7" _msttexthash="51480" _msthash="287">xxxl (xxxl)</option>
						  <option value="8" _msttexthash="68484" _msthash="288">xxxxl</option>
						</select>
						<select id="SelectPcolor" class="select" onchange="Resize();">
						  <option value="red" selected="" _msttexthash="32578" _msthash="289">czerwony</option>
						  <option value="black" _msttexthash="59670" _msthash="290">czarny</option>
						  <option value="blue" _msttexthash="46969" _msthash="291">niebieski</option>
						  <option value="green" _msttexthash="61906" _msthash="292">zielony</option>
						  <option value="magenta" _msttexthash="95407" _msthash="293">magenta</option>
						  <option value="cyan" _msttexthash="143169" _msthash="294">turkus</option>
						  <option value="yellow" _msttexthash="82628" _msthash="295">żółty</option>
						  <option value="gray" _msttexthash="48308" _msthash="296">szary</option>
						</select>
						<select id="SelectPface" class="select" onchange="Resize();">
						  <option value="circle" selected="" _msttexthash="10101" _msthash="297">o</option>
						  <option value="plus">+</option>
						  <option value="diamond">*</option>
						  <option value="square" _msttexthash="876603" _msthash="298">□</option>
						  <option value="cross" _msttexthash="10920" _msthash="299">x</option>
						</select>
						<font _mstmutation="1" _msttexthash="125749" _msthash="300"> Etykieta: </font>
						<input type="checkbox" id="Anno" name="Anno" onchange="Resize();" checked="">
					</div>
				</div>
			</div>
		</div>
		    <table class="calc-table">
        <tbody><tr>
            <td>Dane surowe</td>
            <td><input id="dane-surowe" type="radio" name="dane" checked="checked"></td>
            <td>Dane obliczeniowe</td>
            <td><input id="dane-obliczeniowe" type="radio" name="dane"></td>
        </tr>
    </tbody>
	</table>
	 <div id="div-dane-obliczeniowe" style="display: none;">
        <table class="calc-table">
            <tbody><tr>
                <td>Średnia</td>
                <td><input id="dane-srednia" class="calc-input calc-validation-field-float calc-input-clear" placeholder="Średnia" type="text" autocomplete="off" style="background: rgb(229, 229, 229);"></td>
            </tr>            
            <tr>
                <td>Odchylenie standardowe</td>
                <td><input id="dane-odchylenie" class="calc-input calc-validation-field-float calc-input-clear" placeholder="Odchylenie standardowe" type="text" autocomplete="off" style="background: rgb(229, 229, 229);"></td>
            </tr>            
            <tr>
                <td>Liczebność</td>
                <td><input id="dane-liczebnosc" class="calc-input calc-validation-field-float calc-input-clear" placeholder="Liczebność" type="text" autocomplete="off" style="background: rgb(229, 229, 229);"></td>
            </tr>                                        
        </tbody></table>        
    </div>
    <br>
    <table class="calc-table">
        <tbody><tr>
            <td>Poziom ufności - 0,90</td>
            <td><input id="poziom-090" type="radio" name="poziom"></td>
        </tr>
        <tr>
            <td>Poziom ufności - 0,95</td>
            <td><input id="poziom-095" type="radio" name="poziom" checked="checked"></td>
        </tr>
        <tr>
            <td>Poziom ufności - 0,99</td>
            <td><input id="poziom-099" type="radio" name="poziom"></td>
        </tr>
        <tr>
            <td>Mała próba</td>
            <td><input id="mala-proba" type="radio" name="proba" checked="checked"></td>
        </tr>
        <tr>
            <td>Duża próba</td>
            <td><input id="duza-proba" type="radio" name="proba"></td>
        </tr>
    </tbody></table>  
    <button type="button" id="oblicz" class="calc-btn calc-btn-count">Oblicz</button>
    <button type="button" id="wyczysc" class="calc-btn calc-btn-clear">Wyczyść</button>
    <div class="calc-result" style="display: none;"> 
        <table class="calc-table">            
            <tbody><tr>
                <td>Średnia:</td>
                <td><input id="srednia" class="calc-input" type="text" autocomplete="off" readonly=""></td>
            </tr>  
            <tr>
                <td>Odchylenie standardowe:</td>
                <td><input id="odchylenie" class="calc-input" type="text" autocomplete="off" readonly=""></td>
            </tr>                                                  
            <tr>
                <td> Wariancja min:</td>
                <td><input id="wariancja-min" class="calc-input" type="text" autocomplete="off" readonly=""></td>
            </tr>        
            <tr>
                <td>Wariancja max:</td>
                <td><input id="wariancja-max" class="calc-input" type="text" autocomplete="off" readonly=""></td>
            </tr>  
        </tbody></table>        
    </div>        
		<div class="box-2">
			<div class="table">
				<div class="table-row" title="Data load from file">
					<div class="table-cell" title="Load from file." _msttexthash="277758" _msthash="301"> Załaduj z pliku: </div>
					<div class="table-cell" title="Load measurement data from file to the table.">
						<input onfocus="this.select()" value="Load file" type="file" id="files" name="files[]" class="cButtonL">
					</div>
				</div>
			</div>
			<form name="Formular1" onsubmit="javascript:void(0); return false;">
			<div class="table">
				<div class="table-row" title="Table values">
				</div>
				<div class="table-row" title="Input number of table elements and number of digits.">
					<div class="table-cell" _msttexthash="286104" _msthash="302"> Liczba punktów = </div>
					<div class="table-cell" title="Number of elements">
						<input onfocus="this.select()" type="number" name="n" value="10" class="Eingabe" onchange="drawDiagramm1();">
					</div>
					<div class="table-cell" title="Use the table values for fitting calculations.">
						<input type="button" value="Ustawianie danych" onclick="selectDataSet()" title="set-data" class="cButtonL" _mstvalue="92989" _msthash="303">
					</div>
				</div>
				<div class="table-row" title="Table values">
					<div class="table-cell" title="Move to center.">
						<input type="button" value="Przesuwanie punktów na środek" onclick="MoveS()" title="move-data" class="cButtonL" _mstvalue="394420" _msthash="304">
					</div>
					<div class="table-cell" title="Move to minimal values.">
						<input type="button" value="Przesuwanie punktów do minimalnego" onclick="MoveMin()" title="move-data" class="cButtonL" _mstvalue="426972" _msthash="305">
					</div>
					<div class="table-cell" title="Remove.">
						<input type="button" value="Usunąć" onclick="ReMove()" title="move-data" class="cButtonL" _mstvalue="77779" _msthash="306">
					</div>
				</div>
			</div>
			</form>
			<form name="Formular2" onsubmit="javascript:void(0)" style="margin:0;">
				<div id="Felder" style="clear:both">
				<div class="table">
				<div class="table-row">
				<div class="table-cell" style="text-align: center; padding: 1%;" _msttexthash="357968" _msthash="634">Numer punktu danych</div>
				<div class="table-cell" _msttexthash="532012" _msthash="635">Wartość punktu danych x</div>
				<div class="table-cell" _msttexthash="532350" _msthash="636">Wartość punktu danych y</div>
				</div>
				<div class="table-row">
				<div class="table-cell" style="text-align: center" _msttexthash="4459" _msthash="637">1</div>
				<div class="table-cell">
				<input onfocus="this.select()" class="Eingabe" type="number" name="Lx1">
				</div>
				<div class="table-cell">
				<input onfocus="this.select()" class="Eingabe" type="number" name="Ly1">
				</div>
				</div>
				<div class="table-row">
				<div class="table-cell" style="text-align: center" _msttexthash="4550" _msthash="638">2</div>
				<div class="table-cell">
				<input onfocus="this.select()" class="Eingabe" type="number" name="Lx2">
				</div>
				<div class="table-cell">
				<input onfocus="this.select()" class="Eingabe" type="number" name="Ly2">
				</div>
				</div>
				<div class="table-row">
				<div class="table-cell" style="text-align: center" _msttexthash="4641" _msthash="639">3</div>
				<div class="table-cell"><input onfocus="this.select()" class="Eingabe" type="number" name="Lx3">
				</div>
				<div class="table-cell">
				<input onfocus="this.select()" class="Eingabe" type="number" name="Ly3">
				</div></div><div class="table-row">
				<div class="table-cell" style="text-align: center" _msttexthash="4732" _msthash="640">4</div>
				<div class="table-cell"><input onfocus="this.select()" class="Eingabe" type="number" name="Lx4">
				</div>
				<div class="table-cell">
				<input onfocus="this.select()" class="Eingabe" type="number" name="Ly4">
				</div></div><div class="table-row">
				<div class="table-cell" style="text-align: center" _msttexthash="4823" _msthash="641">5</div>
				<div class="table-cell">
				<input onfocus="this.select()" class="Eingabe" type="number" name="Lx5">
				</div>
				<div class="table-cell">
				<input onfocus="this.select()" class="Eingabe" type="number" name="Ly5">
				</div>
				</div>
				<div class="table-row">
				<div class="table-cell" style="text-align: center" _msttexthash="4914" _msthash="642">6</div>
				<div class="table-cell">
				<input onfocus="this.select()" class="Eingabe" type="number" name="Lx6">
				</div>
				<div class="table-cell">
				<input onfocus="this.select()" class="Eingabe" type="number" name="Ly6">
				</div>
				</div>
				<div class="table-row">
				<div class="table-cell" style="text-align: center" _msttexthash="5005" _msthash="643">7</div>
				<div class="table-cell">
				<input onfocus="this.select()" class="Eingabe" type="number" name="Lx7">
				</div>
				<div class="table-cell">
				<input onfocus="this.select()" class="Eingabe" type="number" name="Ly7">
				</div>
				</div>
				<div class="table-row">
				<div class="table-cell" style="text-align: center" _msttexthash="5096" _msthash="644">8</div>
				<div class="table-cell">
				<input onfocus="this.select()" class="Eingabe" type="number" name="Lx8">
				</div>
				<div class="table-cell">
				<input onfocus="this.select()" class="Eingabe" type="number" name="Ly8">
				</div>
				</div>
				<div class="table-row">
				<div class="table-cell" style="text-align: center" _msttexthash="5187" _msthash="645">9</div>
				<div class="table-cell">
				<input onfocus="this.select()" class="Eingabe" type="number" name="Lx9">
				</div>
				<div class="table-cell">
				<input onfocus="this.select()" class="Eingabe" type="number" name="Ly9">
				</div>
				</div>
				<div class="table-row">
				<div class="table-cell" style="text-align: center" _msttexthash="9451" _msthash="646">10</div>
				<div class="table-cell">
				<input onfocus="this.select()" class="Eingabe" type="number" name="Lx10">
				</div>
				<div class="table-cell">
				<input onfocus="this.select()" class="Eingabe" type="number" name="Ly10">
				</div>
				</div>
				</div>
				</div>
			</form>
			<p _msttexthash="19066645" _msthash="307">Alternatywne wejście jest możliwe z załadowaniem danych z pliku. Wartości mogą być oddzielone przecinkiem, spacją lub średnikiem. Wartości muszą być podane parami x 1,y<sub _istranslated="1"></sub> 
			<sub _istranslated="1">1,x</sub> 2,y<sub _istranslated="1">2</sub>...<sub _istranslated="1"></sub> </p>
		</div>
</body>
</html>
