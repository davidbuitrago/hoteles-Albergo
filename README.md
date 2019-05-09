# hoteles-Albergo
hoteles Albergo
public class localizacion1 extends FragmentActivity implements OnMapReadyCallback,GoogleMap.InfoWindowAdapter {

    private GoogleMap mMap;



    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_localizacion1);
        // Obtain the SupportMapFragment and get notified when the map is ready to be used.
        int status=GooglePlayServicesUtil.isGooglePlayServicesAvailable(getApplicationContext());

        if (status== ConnectionResult.SUCCESS){


        SupportMapFragment mapFragment = (SupportMapFragment) getSupportFragmentManager()
                .findFragmentById(R.id.map);
        mapFragment.getMapAsync(this);
        }else {
            Dialog dialog =GooglePlayServicesUtil.getErrorDialog(status,(Activity)getApplicationContext(),10);
            dialog.show();
        }
    }

   @Override
    public void onMapReady(GoogleMap googleMap) {
        mMap = googleMap;

        mMap.setMapType(GoogleMap.MAP_TYPE_NORMAL);
        UiSettings uiSettings = mMap.getUiSettings();
        uiSettings.setZoomControlsEnabled(true);
        marcas(googleMap);


    }
    public void marcas (GoogleMap googleMap) {
        mMap = googleMap;

        final LatLng punto1 =new LatLng(4.5815455,-74.1409333);
        mMap.addMarker(new MarkerOptions().snippet("Cra. 32 #54a Sur-60 a 54a Sur-2, Bogotá").position(punto1).title("Barberia").icon(BitmapDescriptorFactory.defaultMarker(BitmapDescriptorFactory.HUE_BLUE)));
        mMap.moveCamera(CameraUpdateFactory.newLatLngZoom(punto1,14));
        mMap.setInfoWindowAdapter(this);


        final LatLng punto2 =new LatLng(4.585041,-74.135179);
        mMap.addMarker(new MarkerOptions().snippet("Cra. 32 #50 Sur-54 a 50 Sur-2, Bogotá").position(punto2).title("Barberia").icon(BitmapDescriptorFactory.defaultMarker(BitmapDescriptorFactory.HUE_BLUE)));

        final LatLng punto3 =new LatLng( 4.5709478,-74.1521728);
        mMap.addMarker(new MarkerOptions().snippet("cr 38#63-34 3132586098-3114604320, Bogotá").position(punto3).title("Barberia").icon(BitmapDescriptorFactory.defaultMarker(BitmapDescriptorFactory.HUE_BLUE)));

        final LatLng punto4 =new LatLng(  4.5766293,-74.1534548);
        mMap.addMarker(new MarkerOptions().snippet("Cra. 47 #59b Sur-42 a 59b Sur-2, Bogotá").position(punto4).title("Barberia").icon(BitmapDescriptorFactory.defaultMarker(BitmapDescriptorFactory.HUE_BLUE)));


          final LatLng punto5=new LatLng(4.5787659,-74.154034);
        mMap.addMarker(new MarkerOptions().snippet("Cra. 48g #59a Sur-82 a 59a Sur-52, Bogotá").position(punto5).title("Barberia").icon(BitmapDescriptorFactory.defaultMarker(BitmapDescriptorFactory.HUE_BLUE)));
    }

    @Override
    public View getInfoWindow(Marker marker) {
        return null;
    }

    @Override
    public View getInfoContents(Marker marker) {
        return null;
    }

    @Override
    protected void onResume() {
        super.onResume();
        int errorcode=GoogleApiAvailability.getInstance().isGooglePlayServicesAvailable(this);
        switch (errorcode){
            case ConnectionResult.SERVICE_MISSING:
            case ConnectionResult.SERVICE_VERSION_UPDATE_REQUIRED:
            case ConnectionResult.SERVICE_DISABLED:
                Log.d("Teste","show dialog");
                GoogleApiAvailability.getInstance().getErrorDialog(this, errorcode, 0, new DialogInterface.OnCancelListener() {
                    @Override
                    public void onCancel(DialogInterface dialog) {
                        finish();
                    }
                }).show();
                break;
            case ConnectionResult.SUCCESS:
                Log.d("Teste","Google Play Services up to date ");
                break;
        }
    }
}

