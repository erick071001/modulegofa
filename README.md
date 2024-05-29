# Installation
Add it in your root build.gradle at the end of repositories:
     
     Groovy DSL
     allprojects {
         repositories {
             ...
             maven { url 'https://jitpack.io' }
         }
     }

     Kotlin DSL
     allprojects {
         repositories {
             ...
             maven(url = "https://jitpack.io")
         }
     }

Add the dependency
     
     Groovy DSL
     dependencies {
         implementation 'com.github.gofa-software:gofa-speed-limit:1.0.7'
     }

     Kotlin DSL
     dependencies {
         implementation("com.github.gofa-software:gofa-speed-limit:1.0.7")
     
         val retrofitVersion = "2.9.0"
         implementation("com.squareup.retrofit2:retrofit:$retrofitVersion")
         implementation("com.squareup.retrofit2:converter-gson:$retrofitVersion")
     
         implementation("com.google.code.gson:gson:2.10.1")
     
         val coroutineVersion = "1.7.3"
         implementation("org.jetbrains.kotlinx:kotlinx-coroutines-core:$coroutineVersion")
         implementation("org.jetbrains.kotlinx:kotlinx-coroutines-android:$coroutineVersion")
     
         implementation("androidx.lifecycle:lifecycle-viewmodel-ktx:2.4.0")
     }

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

     Location form "import android.location.Location"
     
# Data model
    data class DatapointModel(
    @SerializedName("id") val id: Int?,
    @SerializedName("compass") val compass: String?,
    @SerializedName("lat") val lat: Double?,
    @SerializedName("lon") val lon: Double?,
    @SerializedName("traffic_sign_id") val trafficSignId: Int?,
    @SerializedName("direction") val direction: Double?,
    )
ex: 
id = 12 with ic_sign_gofa12, id = 13 so icon is ic_sign_gofa13 
Similar to the remaining signs in file ic_sign.zip.
