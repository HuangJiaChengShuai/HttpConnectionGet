public class MainActivity extends Activity {
	private Button btn_duqu;
	
	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_main);
		findViewById(R.id.btn_duqu).setOnClickListener(new  View.OnClickListener() {
			
			@Override
			public void onClick(View v) {
			new AsyncTask<String, Void, Void>(){

				@Override
				protected Void doInBackground(String... params) {
					try {
						URL url=new URL(params[0]);
						URLConnection connection= url.openConnection();
						InputStream is=connection.getInputStream();
						InputStreamReader isr=new InputStreamReader(is,"utf-8");
						BufferedReader br=new BufferedReader(isr);
						String line;
						while((line=br.readLine())!=null){
							System.out.println(line);
						}
						br.close();
						isr.close();
						is.close();
					} catch (MalformedURLException e) {
					
						e.printStackTrace();
					} catch (IOException e) {
						// TODO Auto-generated catch block
						e.printStackTrace();
					}
					return null;
				}
				
			}.execute("http://fanyi.youdao.com/openapi.do?keyfrom=<testHttpGet>&key=<850021564>&type=data&doctype=json&version=1.1&q=good");
				//网易有道API的数据接口
			}
		});
	}
}
