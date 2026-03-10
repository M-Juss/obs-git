Handler handler;

handler.postDelayed(new Runnable() {
		public void run() {
				startActivity(new Intent(this, MainActivity.class));
				finish();
		}

}, 2000)
