# Kotlin Jetpack
A collection of useful extension methods for Android

* [Arguments Bindings](#arguments-bindings)
* [Preferences Bindings](#preferences-bindings)
* [Resources Bindings](#resources-bindings)

# Arguments Bindings
```kotlin
public class ArgumentsFragment : Fragment() {
  public companion object {
    public fun newInstance(): ArgumentsFragment = ArgumentsFragment().apply {
      arguments = Bundle().apply {
        putBoolean("extra_boolean", true)
      }
    }
  }
  
  // Required binding without default value
  val booleanOrThrow: Boolean by bindBooleanArgument("extra_boolean")

  // Required binding with default value
  val booleanOrDefault: Boolean by bindBooleanArgument("extra_boolean", false)

  // Optional binding
  val booleanOrNull: Boolean? by bindOptionalBooleanArgument("extra_boolean")
}
```
Full list of supported bindings:
- `bindBooleanArgument` / `bindOptionalBooleanArgument`
- `bindDoubleArgument` / `bindOptionalDoubleArgument`
- `bindIntArgument` / `bindOptionalIntArgument`
- `bindLongArgument` / `bindOptionalLongArgument`
- `bindStringArgument` / `bindOptionalStringArgument`
- `bindByteArgument` / `bindOptionalByteArgument`
- `bindCharArgument` / `bindOptionalCharArgument`
- `bindFloatArgument` / `bindOptionalFloatArgument`
- `bindParcelableArgument` / `bindOptionalParcelableArgument`
- `bindSerializableArgument` / `bindOptionalSerializableArgument`
- `bindShortArgument` / `bindOptionalShortArgument`

Gradle dependency:
```gradle
compile "com.github.vmironov.jetpack:jetpack-bindings-arguments:0.10.2"
```

# Preferences Bindings
```kotlin
public class PreferencesFragment : Fragment() {
  // Boolean preference
  var boolean: Boolean by bindBooleanPreference("boolean", false)

  // Float preference
  var float: Float by bindFloatPreference("float", 0.0f)

  // Integer preference
  var integer: Int by bindIntPreference("integer", 1)

  // Long preference
  var long: Long by bindLongPreference("long", 1L)

  // String preference
  var string: String by bindStringPreference("string", "default")

  // String Set preference
  var set: Set<String> by bindStringSetPreference("string set")
}
```

The example above uses a default `SharedPreferences` instance. You can always provide a custom one by implementing `PreferencesAware` interface:
```kotlin
public class PreferencesFragment : Fragment() {
  val preferences = PreferencesAware {
    activity.getSharedPreferences("CustomSharedPreferences", Context.MODE_PRIVATE)
  }
  
  var boolean: Boolean by preferences.bindBooleanPreference("boolean", false)
  var float: Float by preferences.bindFloatPreference("float", 0.0f)
  var integer: Int by preferences.bindIntPreference("integer", 1)
  var long: Long by preferences.bindLongPreference("long", 1L)
  var string: String by preferences.bindStringPreference("string", "default")
}
```

Gradle dependency:
```gradle
compile "com.github.vmironov.jetpack:jetpack-bindings-preferences:0.10.2"
```

# Resources Bindings
```kotlin
public class ResourcesFragment : Fragment() {
  // Boolean resource binding
  val boolean: Boolean by bindBooleanResource(R.boolean.boolean_resource)

  // Color resource binding
  val color: Int by bingColorResource(R.color.color_resource)

  // Drawable resource binding #1
  val bitmap: BitmapDrawable by bindDrawableResource(R.drawable.drawable_bitmap)
  
  // Drawable resource binding #2
  val vector: VectorDrawable by bindDrawableResource(R.drawable.drawable_vector)

  // Dimension resource binding
  val dimension: Int by bindDimensionPixelSizeResource(R.dimen.dimen_resource)

  // String resource binding
  val string: String by bindStringResource(R.string.string_resource)
}
```
Full list of supported bindings:
- `bindAnimationResource`
- `bindBooleanResource`
- `bingColorResource`
- `bindColorStateListResource`
- `bindDimensionResource`
- `bindDimensionPixelOffsetResource`
- `bindDimensionPixelSizeResource`
- `bindDrawableResource`
- `bindIntArrayResource`
- `bindIntegerResource`
- `bindLayoutResource`
- `bindMovieResource`
- `bindStringResource`
- `bindStringArrayResource`
- `bindTextResource`
- `bindTextArrayResource`

Gradle dependency:
```gradle
compile "com.github.vmironov.jetpack:jetpack-bindings-resources:0.10.2"
```
