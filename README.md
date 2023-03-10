using System.Collections;
using UnityEngine;

public class AudioVolume : MonoBehaviour
{
    private AudioSource _audio;

    private void Start()
    {
        _audio = GetComponent<AudioSource>(); 
    }

    private void OnTriggerEnter2D(Collider2D collision)
    {
        if (collision.TryGetComponent<Player>(out Player player))
        {
            _audio.Play();
            Coroutine corutineIncrease = StartCoroutine(IncreaseAudio(1));
        }
    }

    private void OnTriggerExit2D(Collider2D collision)
    {
        if (collision.TryGetComponent<Player>(out Player player))
        {
            Coroutine corutineDecrease = StartCoroutine(DecreaseAudio(1));
        }
    }

    private IEnumerator DecreaseAudio(float duraction)
    {
        var volumeDecrease = _audio.volume;
            for (int i = 0; i < 255; i++)
            {
            volumeDecrease = 1f - (1f / 255f * i);
                _audio.volume = volumeDecrease;

                yield return null;
            }
    }

    private IEnumerator IncreaseAudio(float duraction)
    {
        var volumeIncrease = _audio.volume;
        for (int i = 0; i < 255; i++)
        {
            volumeIncrease = 0f + (1f / 255f * i);
            _audio.volume = volumeIncrease;

            yield return null;
        }
    }
}
