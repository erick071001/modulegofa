# Call initGofa() in onCreate() of MainActivity

     private fun initGofa() {
        GofaSpeedLimit.getInstance(this).setGofaKey("key1", "key2")
        GofaSpeedLimit.getInstance(this).setGpsBounds(1)
        GofaSpeedLimit.getInstance(this).setDistanceShowSearchTrafficSign(300)
        if (!GofaSpeedLimit.getInstance(this).maxSpeed.hasObservers()) { 
            Log.d("GofaSpeedLimit", "Speed limit: $it")
            //it: int
        }
        if (!GofaSpeedLimit.getInstance(this).error.hasObservers()) {
            Log.d("GofaSpeedLimit", "OnError: $it")
             //it: String
        }
        if (!GofaSpeedLimit.getInstance(this).listNextBoards.hasObservers()) {
            Log.d("GofaSpeedLimit", "listNextBoards: $it")
             //it: ArrayList(DatapointModel)
        }
        if (!GofaSpeedLimit.getInstance(this).listOtherBoards.hasObservers()) {
            Log.d("GofaSpeedLimit", "listOtherBoards: $it")
             //it: ArrayList(DatapointModel)
        }
        if (!GofaSpeedLimit.getInstance(this).speed.hasObservers()) {
              val newDistance = if (it<=50) 300 else 300 + (it-50)*2
              GofaSpeedLimit.getInstance(this).setDistanceShowSearchTrafficSign(newDistance)
              Log.d("GofaSpeedLimit", "listOtherBoards: $it")
               //it: int
        }
    }

# Call when need update location 
     GofaSpeedLimit.getInstance(this).updateLocation(location)

# 
    data class DatapointModel(
    @SerializedName("id") val id: Int?,
    @SerializedName("compass") val compass: String?,
    @SerializedName("lat") val lat: Double?,
    @SerializedName("lon") val lon: Double?,
    @SerializedName("traffic_sign_id") val trafficSignId: Int?,
    @SerializedName("direction") val direction: Double?,
    )
