package com.danielb.sigwidget;

import android.appwidget.AppWidgetManager;
import android.appwidget.AppWidgetProvider;
import android.content.Context;
import android.telephony.PhoneStateListener;
import android.telephony.SignalStrength;
import android.telephony.TelephonyManager;
import android.widget.RemoteViews;

public class SigWidgetProvider extends AppWidgetProvider {
    
	@Override
    public void onUpdate( Context context, AppWidgetManager appWidgetManager, int[] appWidgetIds )
    {
		final int N = appWidgetIds.length;
        for (int i=0; i<N; i++) {
        	final int appWidgetId = appWidgetIds[i];
        	
        	TelephonyManager telManager;
        	PhoneStateListener signalListener;
        	final RemoteViews views = new RemoteViews(context.getPackageName(), R.layout.main);
        	final AppWidgetManager thisAppWidgetManager = appWidgetManager;
        	
        	signalListener=new PhoneStateListener() {
	           @Override
	           public void onSignalStrengthsChanged(SignalStrength signalStrength) {
	        	   
	        	   Integer mStrength = 0;
	        	   
	        	   if (signalStrength.isGsm())
	                	mStrength = signalStrength.getGsmSignalStrength();
	                else{
	                	int strength = signalStrength.getCdmaDbm();
	                
	                	if (strength < 0){
	                		// convert to asu
	                		mStrength = Math.round((strength + 113f) / 2f);
	                	}
	                }
	        	   
	               views.setTextViewText(R.id.sigStrength, mStrength.toString());

	               thisAppWidgetManager.updateAppWidget(appWidgetId, views);
	           }
        	}; 
        	telManager = (TelephonyManager) context.getSystemService(Context.TELEPHONY_SERVICE);
        	telManager.listen(signalListener, PhoneStateListener.LISTEN_SIGNAL_STRENGTHS);
        
        	appWidgetManager.updateAppWidget(appWidgetId, views);
        }
    }
}
