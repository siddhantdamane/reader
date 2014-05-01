package com.sid.reader;

import android.speech.tts.TextToSpeech;
import android.speech.tts.TextToSpeech.Engine;
import android.speech.tts.TextToSpeech.OnInitListener;

import java.util.Locale;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;
import android.app.Activity;
import android.content.Intent;
import com.sid.reader.R;


public class MainActivity extends Activity {
	
	private EditText ipText;
	private Button speakButton;
	
	private TextToSpeech tts;
	private static int set_var = 1;
	private boolean checkinit = false;


    @Override
    public void onCreate(Bundle savedInstanceState) {

        super.onCreate(savedInstanceState);

        setContentView(R.layout.activity_main);                                
        
     ipText = (EditText)findViewById(R.id.ipText);

        speakButton = (Button) findViewById(R.id.speakButton);
        
                
        speakButton.setOnClickListener(new View.OnClickListener() {

		  public void onClick(View view) {			  			  			  			  
			  if(ipText.getText().toString().trim().length() == 0) { 

				  Toast.makeText(getApplicationContext(), "No text input.", Toast.LENGTH_LONG).show();

				  return;
			  }			  
			  
			  speakip();
		  }
        });
        
        
        testTTS();
    }
    
    private void testTTS()  {

    	Intent intent = new Intent(Engine.ACTION_CHECK_TTS_DATA);

    	startActivityForResult(intent, set_var);
    }

    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    
    	if (requestCode == set_var) {
    	
    		if (resultCode == Engine.CHECK_VOICE_DATA_PASS) {

    			startTTS();
    		}
    		else {
    			Intent installIntent = new Intent(Engine.ACTION_INSTALL_TTS_DATA);
    			startActivity(installIntent);
    		}
    	}
    }
    
    private void startTTS() {
    	tts = new TextToSpeech(this, new OnInitListener() {
    		public void onInit(int status) {
    			if (status == TextToSpeech.SUCCESS) {
    				checkinit = true;
    			}
    			else {
    				//Handle initialization error here
    				checkinit = false;
    			}
    		}
    	});
    }
    
    
    private void speakip() {
    	if(checkinit) {
    		if (tts.isLanguageAvailable(Locale.US) >= 0) 
    			tts.setLanguage(Locale.US);
    		
    		tts.setPitch(0.8f);
    		tts.setSpeechRate(1.1f);
    		
    		tts.speak(ipText.getText().toString(), TextToSpeech.QUEUE_ADD, null);
    	}
    }
    
    
     
    @Override
    public void onDestroy() {
    	if (tts != null) {
    		tts.stop();
    		tts.shutdown();
    	}
    	super.onDestroy();
    }
}
