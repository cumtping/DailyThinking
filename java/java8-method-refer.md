http://zh.lucida.me/blog/java-8-lambdas-insideout-language-features/

frameworks/base/packages/SystemUI/src/com/android/systemui/statusbar/phone/DarkIconDispatcherImpl.java
44          mTransitionsController = new LightBarTransitionsController(context,
45                  this::setIconTintInternal);
94      private void setIconTintInternal(float darkIntensity) {

frameworks/base/packages/SystemUI/src/com/android/systemui/statusbar/phone/LightBarTransitionsController.java
66      public LightBarTransitionsController(Context context, DarkIntensityApplier applier) {
199      /**
200       * Interface to apply a specific dark intensity.
201       */
202      public interface DarkIntensityApplier {
203          void applyDarkIntensity(float darkIntensity);
204      }
